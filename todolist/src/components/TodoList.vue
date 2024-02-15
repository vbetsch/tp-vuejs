<script setup lang="ts">
import {reactive} from "vue";

interface TodoItem {
  title: string,
}

let inputValue: string = ""
let todos: TodoItem[] = reactive([
  {
    title: "Réviser les cours de DevOps"
  },
  {
    title: "Revoir les design pattern"
  },
  {
    title: "Apprendre Vuejs"
  },
])

function clickOnAddTodo() {
  todos.push({
    title: inputValue
  })
}

function clickOnDeleteTodo(todo: TodoItem) {
  todos.splice(
      todos.indexOf(todo),
      1
  );
}
</script>

<template>
  <input id="new-todo" type="text" v-model="inputValue">
  <label for="new-todo">
    <button @click="clickOnAddTodo">Ajouter</button>
  </label>
  <div v-for="todo in todos">
    <p>{{ todo.title }}</p>
    <button @click="clickOnDeleteTodo(todo)">Delete</button>
  </div>
</template>

<style scoped>

</style>
