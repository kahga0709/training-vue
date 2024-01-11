<script setup lang="ts">
import { ref } from 'vue'

defineEmits(['click'])

defineProps({
    imageUrl: String,
})

const test = () => {
    console.log('test');
}

defineExpose({ test })

const isActive = ref<boolean>(false)

</script>

<template>
    <div class="main-container" @click="isActive = !isActive">
        <div class="card" :class="{ 'is-active': isActive }">
            <div class="front">
                <img src="/src/assets/images/icon_back.png" height="50px" width="50px">
            </div>
            <div class="back">
                <img src="/src/assets/images/10.png">
            </div>

        </div>
    </div>
</template>

<style scoped>
.main-container {
    position: absolute;
    width: 100px;
    height: 150px;
    background: none;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

}

.card {
    position: relative;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 10px;
    transform-style: preserve-3d;
    transition: all 0.8s ease;
}

.card.is-active {
    transform: rotateY(180deg);
}

.front {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 10px;
    backface-visibility: hidden;
    overflow: hidden;
    background: #ffc728;
    color: #000;
}

.back {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 10px;
    backface-visibility: hidden;
    overflow: hidden;
    background: #fafafa;
    color: #333;
    text-align: center;
    transform: rotateY(180deg);
}
</style>

