<script setup lang="ts">

const emit = defineEmits(['click']);

const props = defineProps<{
    imageUrl: string
    isFlipped: boolean,
    totalCard: number,
}>()

</script>

<template>
    <div class="card" @click="emit('click')" :style="{
        height: `${(920 - 16 * 4) / Math.sqrt(props.totalCard) - 16}px`,
        width: `${(((920 - 16 * 4) / Math.sqrt(props.totalCard) - 16) * 3) / 4
            }px`,
        perspective: `${((((920 - 16 * 4) / Math.sqrt(props.totalCard) - 16) * 3) / 4) * 2
            }px`,
    }">
        <div class="card__inner" :class="{ 'is-flipped': isFlipped }">
            <div class="card__face card__face--front">
                <div class="card__content" :style="{
                    'background-size': `${(((920 - 16 * 4) / Math.sqrt(props.totalCard) - 16) * 3) /
                        4 /
                        3
                        }px ${(((920 - 16 * 4) / Math.sqrt(props.totalCard) - 16) * 3) /
                        4 /
                        3
                        }px`,
                }"></div>
            </div>
            <div class="card__face card__face--back">
                <div class="card__content">
                    <img :src="imageUrl" height="90%" width="90%">
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
}

.card__inner {
    width: 100%;
    height: 100%;
    transition: transform 0.6s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative
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