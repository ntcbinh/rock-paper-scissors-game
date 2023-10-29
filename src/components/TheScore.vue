<script setup lang="ts">
defineProps(['score'])
</script>
<template>
  <div class="header-score">
    <img src="../assets/images/logo.svg" alt="logo" class="logo" />
    <div class="score">
      <p>SCORE</p>
      <p class="score-number">{{ score }}</p>
    </div>
  </div>
</template>
