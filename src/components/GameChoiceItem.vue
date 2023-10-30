<script setup lang="ts">
defineEmits(['choose'])
defineProps({
  value: {
    type: String,
    default: null
  },
  noColor: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <div
    class="game-content__game-choice"
    :class="[`game-content__game-choice--is-${value}`, noColor ? 'no-color' : '']"
    @click="$emit('choose', value)"
  >
    <div class="game-content__image">
      <slot name="image" />
    </div>
  </div>
</template>

<style lang="css"></style>
