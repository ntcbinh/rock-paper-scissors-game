<script setup lang="ts">
import { ref } from 'vue'

import TheScore from './components/TheScore.vue'
import RulesButton from './components/RulesButton.vue'

import './assets/game.scss'

const isShowModal = ref(false);
const score = ref(1);
const showModal = () => (isShowModal.value = true)
const closeModal = () => (isShowModal.value = false)
</script>

<template>
  <header>
    <TheScore :score="score" />
  </header>

  <main>
    <div class="modal" :class="{ 'modal--isActive': isShowModal }">
      <div class="modal__overlay" @click="closeModal" />
      <div class="modal__content">
        <div class="modal__header">
          <p class="modal__text">Rules</p>
          <button type="button" class="close-modal" @click="closeModal">
            <img src="./assets/images/icon-close.svg" alt="close icon" />
          </button>
        </div>
        <img class="modal__image" src="./assets/images/image-rules.svg" alt="rules image" />
      </div>
    </div>
    <div class="game-content">
      <div class="game-content__bg" />
      <div class="game-content__game-choice game-content__game-choice--isPaper">
        <div class="game-content__image">
          <img src="./assets/images/icon-paper.svg" alt="paper choice" />
        </div>
      </div>
      <div class="game-content__game-choice game-content__game-choice--isRock">
        <div class="game-content__image">
          <img src="./assets/images/icon-rock.svg" alt="rock choice" />
        </div>
      </div>
      <div class="game-content__game-choice game-content__game-choice--isScissors">
        <div class="game-content__image">
          <img src="./assets/images/icon-scissors.svg" alt="scissors choice" />
        </div>
      </div>
    </div>
  </main>

  <footer>
    <RulesButton @click="showModal" />
  </footer>
</template>
