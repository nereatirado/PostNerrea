<template>
  <div class="post">
    <span>{{ entrada.body }}</span>
    <p>{{ formatearFecha(entrada.dataCreacio) }}</p>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';
import type Entry from '@/types/Entry';

const props = defineProps({
  entrada: {
    type: Object as () => Entry,
    required: true,
  },
});

const formatearFecha = (dateTime: string | number | Date) => {
  const fecha = new Date(dateTime);

  const opcionesFecha = { day: 'numeric', month: 'numeric', year: 'numeric' };
  const opcionesHora = { hour: 'numeric', minute: 'numeric' };

  const fechaFormateada = fecha.toLocaleDateString('es-ES', opcionesFecha);
  const horaFormateada = fecha.toLocaleTimeString('es-ES', opcionesHora);

  return `${fechaFormateada} a las ${horaFormateada}`;
};
</script>
