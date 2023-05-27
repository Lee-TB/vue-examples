<script setup>
import AnotherButton from './AnotherButton.vue';
import CustomLayout from './CustomLayout.vue';
import MyButton from './MyButton.vue';
import UseAttrs from './UseAttrs.vue';

function onClick() {
  alert('something');
}

function changeValue() {
  console.log('change something');
}

function doSomething() {
  console.log('do something');
}
</script>

<template>
  <MyButton class="red large text-white" @click="onClick" />
  <AnotherButton class="red" @click="onClick" />
  <CustomLayout id="custom-layout" @click="changeValue" />
  <UseAttrs class="red" @click="doSomething" />
</template>

<style>
.red {
  background: red;
}

.large {
  padding: 4px 8px;
}

.text-white {
  color: white;
}
</style>
