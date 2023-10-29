<script setup lang="ts">
const emit = defineEmits(['click'])
const showRules = () => emit('click')
</script>

<template>
  <div>
    <button type="button" @click="showRules" class="rules-button">RULES</button>
  </div>
</template>
