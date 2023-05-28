<script setup>
import { ref, watchEffect } from 'vue';
const API_URL = `https://api.github.com/repos/vuejs/core/commits?per_page=3&sha=`;
const branches = ['main', 'v2-compat'];
const currentBranch = ref(branches[0]);
const commits = ref(null);

watchEffect(async () => {
  const url = `${API_URL}${currentBranch.value}`;
  commits.value = await (await fetch(url)).json();
});

function truncate(v) {
  const newline = v.indexOf('\n');
  return newline > 0 ? v.slice(0, newline) : v;
}

function formatDate(v) {
  return v.replace(/T|Z/g, ' ');
}
</script>

<template>
  <h1>Latest Vue Core commits</h1>

  <template v-for="branch in branches">
    <input type="radio" v-model="currentBranch" :value="branch" :id="branch" />
    <label :for="branch">{{ branch }}</label>
  </template>

  <p>vuejs/vue@{{ currentBranch }}</p>

  <ul v-if="commits.length">
    <li v-for="{ html_url, sha, author, commit } of commits">
      <a :href="html_url" target="_blank" class="commit">{{
        sha.slice(0, 7)
      }}</a>
      - <span>{{ truncate(commit.message) }}</span>
      <br />
      by
      <span class="author">
        <a :href="author.html_url" target="_blank">{{ commit.author.name }}</a>
      </span>
      at <span class="date">{{ formatDate(commit.author.date) }}</span>
    </li>
  </ul>
</template>

<style>
a {
  text-decoration: none;
  color: #42b883;
}
li {
  line-height: 1.5em;
  margin-bottom: 20px;
}
.author,
.date {
  font-weight: bold;
}
</style>
