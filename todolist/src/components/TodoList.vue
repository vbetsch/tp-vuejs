<script setup lang="ts">
import {reactive} from "vue";

let inputValue = ""
let todos = reactive([
  "Réviser les cours de DevOps",
  "Créer une pipeline CI pour le projet Ruptik",
  "Revoir les design pattern",
  "Apprendre Vuejs",
  "Créer un script bash pour push la visu",
  "Créer un site sur React"
])

function clickOnAddTodo() {
  todos.push(inputValue);
}
</script>

<template>
  <input id="new-todo" type="text" v-model="inputValue">
  <label for="new-todo">
    <button @click="clickOnAddTodo">Ajouter</button>
  </label>
  <div v-for="todo in todos">
    {{ todo }}
  </div>
</template>

<style scoped>

</style>
