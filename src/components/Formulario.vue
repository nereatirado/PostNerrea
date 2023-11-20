<template>
    <div class="form-container">
      <header>
        <div class="logo-container">
          <h1>My Journal</h1>
          <img src="../img/logo.png" alt="Logo" />
        </div>
      </header>
      <form @submit.prevent="gestionarSubmit">
        <textarea v-model="body" @input="limitarTexto" name="" id="" cols="50" rows="10"></textarea>
        <div class="emoji-container">
          <Emoticonos v-model="emoji"></Emoticonos>
        </div>
        <div class="char-count">
          <span>{{ charCount }} / {{ maximoCaracteres }}</span>
          <p v-if="excedeLimite" class="error-message">¡Has excedido el límite de caracteres!</p>
        </div>
        <button type="submit" :disabled="excedeLimite">Publicar</button>
      </form>
    </div>
  </template>
  
  <script setup lang="ts">
  import { computed, ref, defineEmits } from 'vue';
  import Emoticonos from '@/components/Emoticonos.vue';
  import type Entry from '@/types/Entry.ts';
  import type Emoji from '@/types/Emojis.ts';
  
  const emit = defineEmits<{
    (e: '@create', entry: Entry): void;
  }>();
  
  const maximoCaracteres = 280;
  const body = ref('');
  const emoji = ref<Emoji | null>(null);
  const charCount = computed(() => body.value.length);
  const excedeLimite = computed(() => charCount.value > maximoCaracteres);
  
  const limitarTexto = () => {
    if (body.value.length > maximoCaracteres) {
      body.value = body.value.slice(0, maximoCaracteres);
    }
  };
  
  const gestionarSubmit = () => {
    if (!excedeLimite.value) {
      emit('@create', {
        body: body.value,
        emoji: emoji.value,
        dataCreacio: new Date(),
        userId: 1,
        id: Math.random(),
      });
  
      body.value = '';
      emoji.value = null;
    }
  };
  </script>
  
  <style>
  .form-container {
    max-width: 600px;
    margin: 0 auto;
  }
  
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  
  .logo-container {
    display: flex;
    align-items: center;
  }
  
  img {
    max-height: 50px;
    margin-right: 10px;
    margin-left: 6px;
  }
  
  textarea {
    width: 100%;
    margin-bottom: 10px;
  }
  
  .emoji-container {
    margin-bottom: 10px;
  }
  
  .char-count {
    text-align: right;
    margin-bottom: 10px;
  }
  
  button {
    background-color: #4caf50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  
  .error-message {
    color: red;
    margin-top: 5px;
  }
  </style>
  