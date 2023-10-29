<script setup lang="ts">
import { ref } from 'vue'

import GameChoiceItem from './components/GameChoiceItem.vue'
import TheScore from './components/TheScore.vue'
import RulesButton from './components/RulesButton.vue'
import RulesModal from './components/RulesModal.vue'

import './assets/game.scss'

const isShowModal = ref(false)
const score = ref(1)
const showModal = () => (isShowModal.value = true)
const closeModal = () => (isShowModal.value = false)
const getImg = (img: string) => {
  return new URL(`./assets/images/icon-${img}.svg`, import.meta.url).href
}
const chooseItem = (item: string) => console.log(item)
</script>

<template>
  <header>
    <TheScore :score="score" />
  </header>

  <main>
    <RulesModal :is-show="isShowModal" @close="closeModal" />
    <div class="game-content">
      <div class="game-content__bg" />
      <GameChoiceItem
        v-for="(item, index) in ['paper', 'rock', 'scissors']"
        :key="index"
        :value="item"
        @choose="chooseItem"
      >
        <template #image>
          <img :src="getImg(item)" :alt="`${item} choice`" />
        </template>
      </GameChoiceItem>
    </div>
  </main>

  <footer>
    <RulesButton @click="showModal" />
  </footer>
</template>
