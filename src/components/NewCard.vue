<script setup lang="ts">

const emit = defineEmits(['click']);

defineProps({
    imageUrl: String,
    isFlipped: Boolean,
    isActive: Boolean,
});
</script>

<template>
    <div class="card" @click="emit('click')">
        <div class="card__inner" :class="{ 'is-flipped': isFlipped }">
            <div class="card__face card__face--front">
                <div class="card__content"></div>
            </div>
            <div class="card__face card__face--back">
                <div class="card__content">
                    <img :src="imageUrl">
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.card {
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
    height: 198px;
    width: 148.5px;
    perspective: 297px;
}

.card__inner {
    width: 100%;
    height: 100%;
    transition: transform 0.6s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative
}

.card.disabled .card__inner {
    cursor: default
}

.card__inner.is-flipped {
    transform: rotateY(-180deg)
}

.card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 3px 18px 3px rgba(0, 0, 0, .2)
}

.card__face--front .card__content {
    background: url("../assets/images/icon_back.png") no-repeat center center;
    height: 100%;
    width: 100%;
    background-size: 49.5px 49.5px;
}

.card__face--back {
    background-color: var(--light);
    transform: rotateY(-180deg)
}

.card__face--back .card__content {
    background-position: 50%;
    background-repeat: no-repeat;
    background-size: contain;
    height: 100%;
    width: 100%
}
</style>