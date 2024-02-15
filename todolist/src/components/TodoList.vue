<script setup lang="ts">
import {reactive} from "vue";
import Todo from "./TodoItem.vue";

let inputNewValue = ""
let todos: TodoItemType[] = reactive([])

function clickOnAddTodo() {
    if (inputNewValue !== "") {
        todos.push({
            title: inputNewValue
        })
        inputNewValue = ""
    }
}

function clickOnDeleteTodo(todo: TodoItemType) {
    todos.splice(
        todos.indexOf(todo),
        1
    );
}
</script>

<template>
    <input id="new-todo" type="text" v-model="inputNewValue" @keydown.enter="clickOnAddTodo" autofocus>
    <label for="new-todo">
        <button @click="clickOnAddTodo">Add</button>
    </label>
    <div v-for="todo in todos" :key="todos.indexOf(todo)">
        <Todo :todo="todo"/>
        <button @click="clickOnDeleteTodo(todo)">Delete</button>
    </div>
</template>

<style scoped></style>
