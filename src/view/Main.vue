<script setup lang="ts">
import ModeButton from '../components/ModeButton.vue';

const modes = [
    {
        title: '4X4',
        mode: 'Easy',
        totalCard: 16,
    },
    {
        title: '6X6',
        mode: 'Normal',
        totalCard: 36,
    },
    {
        title: '8X8',
        mode: 'Hard',
        totalCard: 54,
    },
    {
        title: '10X10',
        mode: 'Super Hard',
        totalCard: 100,
    },
]
const emit = defineEmits(['click']);

const onSelectedMode = (totalCard: number) => {
    emit('click', totalCard);
}

</script>

<template>
    <h1>POKE MEMORIES</h1>
    <p>Select mode to start game</p>

    <div class="modes">
        <ModeButton v-for="(m, index) in modes" :title="m.title" :mode="m.mode" :key="index"
            @click="onSelectedMode(m.totalCard)" />
    </div>
</template>

<style scoped>
.modes {
    display: flex;
    margin-top: 2rem;
}
</style> 