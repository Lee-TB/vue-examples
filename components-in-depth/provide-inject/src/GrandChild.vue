<script setup>
import { inject } from 'vue';

const message = inject('message', 'default value');
</script>

<template>
  <div>Message in Grand Child is: {{ message }}</div>
</template>
