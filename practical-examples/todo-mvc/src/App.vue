<script setup>
import { ref, watchEffect, computed } from 'vue';

const STORAGE_KEY = 'todos-vuejs-2.0';
const todos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY)) || []);
const visibility = ref('all');

const filters = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed),
};

watchEffect(() => {
  window.localStorage.setItem(STORAGE_KEY, JSON.stringify(todos.value));
});

let id = 0;

function addTodo(e) {
  const value = e.target.value.trim();
  todos.value.push({ id: id++, text: value, completed: false });
}

function removeTodo(todo) {
  const index = todos.value.indexOf(todo);
  todos.value.splice(index, 1);
}

const editedTodo = ref(null);
let beforeEditCache = '';
function editTodo(todo) {
  beforeEditCache = todo.text;
  editedTodo.value = todo;
}

function toggleAll() {
  const allCompleted = todos.value.every((todo) => todo.completed);
  todos.value.forEach((todo) => (todo.completed = !allCompleted));
}

function doneEdit(todo) {
  if (!editedTodo.value) return;
  editedTodo.value = null;
  todo.text = todo.text.trim();
}

function cancelEdit(todo) {
  editedTodo.value = null;
  todo.text = beforeEditCache;
}

function onHashChange() {
  const route = window.location.hash.replace(/#\/?/, '');
  if (filters[route]) {
    visibility.value = route;
  } else {
    window.location.hash = ''; // default
    visibility.value = 'all';
  }
}
onHashChange();
window.addEventListener('hashchange', onHashChange);

const filteredTodos = computed(() => filters[visibility.value](todos.value)); // filters is a list of functions
const remaining = computed(() => filters.active(todos.value).length); // number of active todos

function removeCompleted() {
  todos.value = filters.active(todos.value);
}
</script>

<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input
        type="text"
        class="new-todo"
        placeholder="What needs to be done?"
        autofocus
        @keyup.enter="addTodo"
      />
    </header>
    <section class="main">
      <input
        type="checkbox"
        id="toggle-all"
        class="toggle-all"
        @change="toggleAll"
      />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <li
          class="todo"
          v-for="todo in filteredTodos"
          :key="todo.id"
          :class="{ completed: todo.completed, editing: todo === editedTodo }"
        >
          <div class="view">
            <input type="checkbox" class="toggle" v-model="todo.completed" />
            <label @dblclick="editTodo(todo)">{{ todo.text }}</label>
            <button @click="removeTodo(todo)" class="destroy"></button>
          </div>
          <input
            v-if="todo === editedTodo"
            type="text"
            class="edit"
            v-model="todo.text"
            @blur="doneEdit(todo)"
            @keyup.enter="doneEdit(todo)"
            @keyup.escape="cancelEdit(todo)"
          />
        </li>
      </ul>
    </section>
    <footer class="footer">
      <span class="todo-count">
        <strong>{{ remaining }}</strong>
        <span>{{ remaining === 1 ? ' item' : ' items' }} left</span>
      </span>
      <ul class="filters">
        <li>
          <a href="#/all" :class="{ selected: visibility === 'all' }">All</a>
        </li>
        <li>
          <a href="#/active" :class="{ selected: visibility === 'active' }"
            >Active</a
          >
        </li>
        <li>
          <a
            href="#/completed"
            :class="{ selected: visibility === 'completed' }"
            >Completed</a
          >
        </li>
      </ul>
      <button
        class="clear-completed"
        @click="removeCompleted"
        v-show="todos.length > remaining"
      >
        Clear completed
      </button>
    </footer>
  </section>
</template>

<style>
@import 'https://unpkg.com/todomvc-app-css@2.4.1/index.css';
label[for='toggle-all'] {
  cursor: pointer;
}
.destroy {
  cursor: pointer;
}
</style>
