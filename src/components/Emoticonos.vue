<!-- Emoticonos.vue -->
<template>
    <div class="emoticonos">
      <!-- Aquí puedes poner tus emoticonos o usar un componente de emoticonos -->
      <button @click="seleccionarEmoticono('😊')">😊</button>
      <button @click="seleccionarEmoticono('😂')">😂</button>
      <!-- Agrega más botones o utiliza un componente de emoticonos aquí -->
    </div>
  </template>
  
  <script setup lang="ts">
  import { defineProps, defineEmits } from 'vue';
  
  const emit = defineEmits<{
    (e: 'seleccionarEmoticono', emoticono: string): void;
  }>();
  
  const seleccionarEmoticono = (emoticono: string) => {
    emit('seleccionarEmoticono', emoticono);
  };
  </script>
  
  <style scoped>
  .emoticonos {
    display: flex;
    justify-content: space-around;
    margin-top: 10px;
  }
  </style>
  