<script setup lang="ts">
defineProps<{
    title: string
    mode: string
}>()

const emit = defineEmits(['click'])
</script>

<template>
    <button class="mode-button" @click="emit('click')">
        <span class="span-title">{{ title }}</span>
        <span class="span-rank"> {{ mode }}</span>
    </button>
</template>

<style scoped>
.mode-button {
    width: 150px;
    height: 150px;
    background: transparent;
    box-shadow: none;
    border: 1px solid var(--light);
    color: var(--light);
    display: flex;
    flex-direction: column;
    border-radius: 1rem;
    margin: 0 1rem;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background .3s ease-in-out
}

.mode-button:hover {
    background-color: var(--light);
    color: var(--dark)
}

.span-title {
    font-size: 2rem
}

.pan-rank {
    display: block;
    font-size: 1.25rem;
    margin-top: .5rem
}
</style>