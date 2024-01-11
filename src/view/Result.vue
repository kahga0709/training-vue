<script setup lang="ts">
import { ref } from 'vue'

defineProps<{
    timer: number,
}>()

const emit = defineEmits(['click'])

const contacts = ref<any[]>([
    { link: 'https://www.facebook.com/', icon: 'https://img.icons8.com/color/48/000000/facebook.png' },
    { link: 'https://www.facebook.com/', icon: 'https://img.icons8.com/fluent/48/000000/twitter.png' },
    { link: 'https://www.facebook.com/', icon: 'https://img.icons8.com/fluent/48/000000/instagram-new.png' },
    { link: 'https://www.facebook.com/', icon: 'https://img.icons8.com/fluency/48/000000/gmail-new.png' },
    { link: 'https://www.facebook.com/', icon: 'https://img.icons8.com/color/48/000000/youtube-play.png' },
]);

</script>

<template>
    <h1>✨ Congratulations ✨</h1>
    <h2>🍓🍓🍓🍓🍓🍓🍓🍓🍓🍓🍓🍓</h2>
    <h3>{{ timer }} seconds</h3>

    <button class="button" @click="emit('click')">
        Start Again
    </button>

    <h5>Connect with me</h5>
    <div>
        <a v-for="(item, index) in contacts" :key="index" :href="item.link">
            <img :src="item.icon">
        </a>
    </div>
</template>

<style scoped>
.button {
    font: var(--font);
    background: transparent;
    box-shadow: none;
    border: 1px solid var(--light);
    color: var(--light);
    margin: 1rem;
    padding: 1rem 1.25rem;
    border-radius: 0.5rem;
    font-size: 1.25rem;
    cursor: pointer;
    transition: background .3s ease-in-out;
}

.button:hover {
    background-color: var(--light);
    color: var(--dark)
}
</style>