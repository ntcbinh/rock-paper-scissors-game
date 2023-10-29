<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps(['isShow'])
const isShowModal = computed(() => props.isShow)
const emit = defineEmits(['close'])
</script>

<template>
  <div class="modal" :class="{ 'modal--isActive': isShowModal }">
    <div class="modal__overlay" @click="emit('close')" />
    <div class="modal__content">
      <div class="modal__header">
        <p class="modal__text">Rules</p>
        <button type="button" class="close-modal" @click="emit('close')">
          <img src="../assets/images/icon-close.svg" alt="close icon" />
        </button>
      </div>
      <img class="modal__image" src="../assets/images/image-rules.svg" alt="rules image" />
    </div>
  </div>
</template>
