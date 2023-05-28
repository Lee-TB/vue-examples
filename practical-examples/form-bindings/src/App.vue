<script setup>
import { ref } from 'vue';

const text = ref('Edit me');
const checked = ref(false);
const checkedNames = ref([]);
const picked = ref('One');
const selected = ref('A');
const multiSelected = ref(['C']);
</script>

<template>
  <h2>Text input</h2>
  <input type="text" v-model="text" /> {{ text }}

  <h2>Checkbox</h2>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">Checked: {{ checked }}</label>

  <h2>Multi checkbox</h2>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
  <p>Checked Names: <pre>{{ checkedNames }}</pre></p>

  <h2>Radio</h2>
  <input type="radio" id="one" value="One" v-model="picked">
  <label for="one">One</label>
  <input type="radio" id="two" value="Two" v-model="picked">
  <label for="two">Two</label>

  <h2>Select</h2>
  <select v-model="selected">
    <option value="" disabled>Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ JSON.stringify(selected) }}</span>

  <h2>Multi Select</h2>
  <select v-model="multiSelected" :style="{width: '100px'}" multiple>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: <pre>{{ multiSelected }}</pre></span>


</template>
