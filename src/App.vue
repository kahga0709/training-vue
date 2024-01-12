<script setup lang="ts">
import { ref } from 'vue'
import Main from './view/Main.vue';
import Interact from './view/Interact.vue';
import Result from './view/Result.vue';

enum Page {
  Main,
  Interact,
  Result,
}

const statusMatch = ref<Page>(Page.Main);

const total = ref<number>(0);
const level = ref<number>(0);
const timer = ref<number>(0);

const initGame = (mode: any) => {
  total.value = mode.totalCard;
  level.value = mode.level;
  navigateTo(Page.Interact);
}

const navigateTo = (page: Page) => {
  statusMatch.value = page;
}

const getTime = (time: number) => {
  timer.value = time;
}
</script>

<template>
  <div class="screen">
    <Main v-if="statusMatch === Page.Main" @click="(mode) => initGame(mode)" />
    <Interact v-else-if="statusMatch === Page.Interact" :totalCard="total" @goResult="navigateTo(Page.Result)"
      @getTime="getTime($event)" :level="level" />
    <Result v-else-if="statusMatch === Page.Result" :timer="timer" @click="navigateTo(Page.Main)" />
  </div>
</template>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--dark);
}
</style> 

