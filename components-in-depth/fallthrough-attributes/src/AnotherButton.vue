<script setup>
import MyButton from './MyButton.vue';
</script>

<template>
  <!-- This will be called nested component inheritance -->
  <!-- The fallthrough attributes received 
    by AnotherButton will be automatically forwarded to <MyButton />  -->
  <MyButton />
</template>
