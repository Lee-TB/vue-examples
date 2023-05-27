<script setup>
import { ref } from 'vue';
import CustomInput1 from './CustomInput1.vue';
import CustomInput2 from './CustomInput2.vue';
import MyComponent from './MyComponent.vue';
import UserName from './UserName.vue';

const searchText1 = ref('');
const searchText2 = ref('');
const title = ref('v-model argument example');
const firstName = ref('');
const lastName = ref('');
</script>

<template>
  <h2>Custom input 1</h2>
  <div>
    <CustomInput1
      :modelValue="searchText1"
      @update:modelValue="(newValue) => (searchText1 = newValue)"
    />
    {{ searchText1 }}
  </div>
  <div>
    <CustomInput1 v-model:modelValue="searchText2" />
    {{ searchText2 }}
  </div>

  <h2>Custom input 2</h2>
  <div>
    <CustomInput2
      :modelValue="searchText1"
      @update:modelValue="(newValue) => (searchText1 = newValue)"
    />
    {{ searchText1 }}
  </div>
  <div>
    <CustomInput2 v-model="searchText2" />
    {{ searchText2 }}
  </div>
  <h2>v-model arguments</h2>
  <MyComponent v-model:title="title" />
  {{ title }}

  <h2>UserName</h2>
  <UserName
    v-model:firstName.capitalize="firstName"
    v-model:lastName="lastName"
  />
  <div>
    <pre>
      {{ { firstName, lastName } }}
    </pre>
  </div>
</template>
