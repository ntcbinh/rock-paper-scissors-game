<script setup lang="ts">
import { computed, ref } from 'vue'

import GameChoiceItem from './components/GameChoiceItem.vue'
import TheScore from './components/TheScore.vue'
import RulesButton from './components/RulesButton.vue'
import RulesModal from './components/RulesModal.vue'

import './assets/game.scss'

const isShowModal = ref(false)
const score = ref(0)
const showModal = () => (isShowModal.value = true)
const closeModal = () => (isShowModal.value = false)
const gameChoices = computed(() => ['paper', 'scissors', 'rock'])
const getImg = (img: string) => {
  return new URL(`./assets/images/icon-${img}.svg`, import.meta.url).href
}
const chooseItem = (item: string) => {
  selectedChoice.value = item
  startCountdown()
}
const getRandomNumber = () => Math.floor(Math.random() * 3)
const selectedChoice = ref()
const randomResult = ref()
const status = ref('')
const countdown = ref<number>(4)
const showResult = (userChoice: string, computerChoice: string) => {
  if (userChoice === computerChoice) {
    status.value = 'DRAW'
  } else if (
    (userChoice === gameChoices.value[0] && computerChoice === gameChoices.value[1]) ||
    (userChoice === gameChoices.value[1] && computerChoice === gameChoices.value[2]) ||
    (userChoice === gameChoices.value[2] && computerChoice === gameChoices.value[0])
  ) {
    if (score.value > 0) {
      score.value -= 1
    }
    status.value = 'YOU LOSE'
  } else {
    score.value += 1
    status.value = 'YOU WIN'
  }
}

const startCountdown = () => {
  countdown.value -= 1

  if (countdown.value) {
    setTimeout(() => startCountdown(), 600)
  } else {
    randomResult.value = gameChoices.value[getRandomNumber()]

    showResult(selectedChoice.value, randomResult.value)
    countdown.value = 4
  }
}

const playAgain = () => {
  selectedChoice.value = null
  randomResult.value = null
}
</script>

<template>
  <header>
    <TheScore :score="score" />
  </header>

  <main>
    <RulesModal :is-show="isShowModal" @close="closeModal" />
    <div class="game-content">
      <div class="game-content__bg" v-show="!selectedChoice && !randomResult" />
      <template v-if="!selectedChoice && !randomResult">
        <GameChoiceItem
          v-for="(item, index) in gameChoices"
          :key="index"
          :value="item"
          @choose="chooseItem"
        >
          <template #image>
            <img :src="getImg(item)" :alt="`${item} choice`" />
          </template>
        </GameChoiceItem>
      </template>
      <div v-else class="game-result">
        <div class="result-item">
          <div class="title">YOUR CHOICE</div>
          <GameChoiceItem :value="selectedChoice">
            <template #image>
              <img :src="getImg(selectedChoice)" :alt="`${selectedChoice} choice`" />
            </template>
          </GameChoiceItem>
        </div>
        <div class="status">
          <div v-show="countdown === 4 && selectedChoice">
          {{ status }}
          <button class="play-again" type="button" @click="playAgain">PLAY AGAIN</button>
        </div>
        </div>
        <div class="result-item">
          <div class="title">COMPUTER CHOICE</div>
          <GameChoiceItem :value="randomResult">
            <template #image>
              <img
                v-if="randomResult"
                :src="getImg(randomResult)"
                :alt="`${randomResult} choice`"
              />
              <span v-else class="count-down">{{ countdown }}</span>
            </template>
          </GameChoiceItem>
        </div>
      </div>
    </div>
  </main>

  <footer>
    <RulesButton @click="showModal" />
  </footer>
</template>
