<script setup lang="ts">
import { reactive } from "vue";
import Formulario from "./components/Formulario.vue";
import Enviat from "./components/PostEnviat.vue"
import type Entry from "./types/Entry";

const entrades: Entry[] = reactive([])

const manipularPost = (entradaPost: Entry) => {
    entrades.push(entradaPost) 
}


</script>

<template>
    <div class="principal">
        <Formulario @@create="manipularPost"></Formulario>
    </div>
    <!--Para cada post te hace un li nuevo-->
    <ul>
        <li v-for="entrada in entrades" :key="entrada.id"><Enviat></Enviat></li>
    </ul>
</template>

<style>
.principal{
    width: 800px;
}
</style>
