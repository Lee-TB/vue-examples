<script setup>
import { ref } from 'vue';

const message = ref('Hello world');

function reverseMessage() {
  message.value = message.value.split('').reverse().join('');
}

function notify() {
  alert('navigation was prevented');
}
</script>

<template>
  <div>
    <h1>
      {{ message }}
    </h1>

    <button v-on:click="reverseMessage">reverse message</button>

    <button @click="message += `!`">append "!"</button>

    <a href="https://vuejs.org" @click.prevent="notify" target="_blank">
      A link with e.preventDefault()
    </a>
  </div>
</template>

<style>
button,
a {
  display: block;
  margin-bottom: 1em;
}
</style>
