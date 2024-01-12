<script setup lang="ts" >
import { onBeforeMount, onMounted, ref } from 'vue'
import NewCard from '../components/NewCard.vue';

interface CardModel {
    value: number,
    isFlipped: boolean,
    isActive: boolean,
}

const emit = defineEmits(['goResult', 'getTime'])

const props = defineProps<{
    totalCard: number,
    level: number,
}>()
const cards = ref<CardModel[]>([]);

let point: number = 0;
let selectedList: { value: number, index: number }[] = []
let second = 0;

onBeforeMount(() => {
    generateCard(props.totalCard);
})

onMounted(() => {
    setInterval(() => {
        second++
    }, 1000);
})

const generateCard = (totalCard: number) => {
    const arr1 = Array.from({ length: totalCard / 2 }, (_, i) => i + 1)
    const arr = [...arr1, ...arr1]
    shuffle(arr);

    for (let i = 0; i < arr.length; i++) {
        cards.value.push({
            value: arr[i],
            isFlipped: false,
            isActive: true,
        })
    }

}

const shuffle = (array: number[]) => {
    let currentIndex = array.length, randomIndex;

    while (currentIndex > 0) {

        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        [array[currentIndex], array[randomIndex]] = [
            array[randomIndex], array[currentIndex]];
    }

    return array;
}

function removeSelectedCard(
    array: { value: number, index: number }[],
    elem: { value: number, index: number },
) {
    var index = array.indexOf(elem);
    if (index > -1) {
        array.splice(index, 1);
    }
}

const onSelectCard = (index: number) => {

    const item = cards.value[index];

    if (!item.isActive) return

    if (item.isFlipped) {
        removeSelectedCard(selectedList, { value: item.value, index: index })
        cards.value[index].isFlipped = false;
    } else {
        selectedList.push({ value: item.value, index: index })
        cards.value[index].isFlipped = true;
    }

    if (selectedList.length === 2) {
        const item1 = selectedList[0]
        const item2 = selectedList[1]

        if (item1.value === item2.value) {
            cards.value[item1.index].isActive = false;
            cards.value[item2.index].isActive = false;
            // Check win
            point++
            if (point === props.totalCard / 2) {
                emit('goResult')
                emit('getTime', second)
            }
        } else {
            setTimeout(() => {
                cards.value[item1.index].isFlipped = false;
                cards.value[item2.index].isFlipped = false;
            }, 500)
        }
        // reset selected
        selectedList = [];
    }
}
</script> 

<template>
    <div class="interact">
        <div class="interact__inner" :style="{
            width: `${((((920 - 16 * 4) / Math.sqrt(totalCard) - 16) * 3) / 4 +
                16) *
                Math.sqrt(totalCard)
                }px`,
        }">
            <NewCard v-for="(card, index) in cards " :key="index" :imageUrl="`/src/assets/images/${card.value}.png`"
                :isFlipped="card.isFlipped" :totalCard="totalCard" @click="onSelectCard(index)" />
        </div>
    </div>
</template>

<style scoped>
.interact {
    width: 100%;
    height: auto;
    position: absolute;
    top: 0;
    left: 0;
    background-color: var(--dark);
}

.interact__inner {
    width: calc(424px);
    display: flex;
    flex-wrap: wrap;
    margin: 2rem auto;
}
</style>

