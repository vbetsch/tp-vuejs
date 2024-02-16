<script setup lang="ts">
import {reactive, Ref, ref} from "vue";
import Todo from "./TodoItem.vue";

let inputNewValue: Ref<string> = ref("")
let todos: TodoItemType[] = reactive([])

function clickOnAddTodo() {
    if (inputNewValue.value !== "") {
        todos.push({
            title: inputNewValue.value,
            isSelected: false
        })
        inputNewValue.value = ""
    }
}

function clickOnDeleteTodo(todo: TodoItemType) {
    todos.splice(
        todos.indexOf(todo),
        1
    );
}

function clickOnDeleteSelectedTodos() {
    const selectedTodos = todos.filter((todo: TodoItemType) => todo.isSelected)
    if (selectedTodos.length) {
        selectedTodos.map((todo) => clickOnDeleteTodo(todo))
    }
}
</script>

<template>
    <input id="new-todo" type="text" v-model="inputNewValue" @keydown.enter="clickOnAddTodo" autofocus>
    <label for="new-todo">
        <button @click="clickOnAddTodo">Add</button>
    </label>
    <button @click="clickOnDeleteSelectedTodos">Delete selected</button>
    <div class="todo" v-for="todo in todos" :key="todos.indexOf(todo)">
        <Todo :todo="todo"/>
        <button @click="clickOnDeleteTodo(todo)">Delete</button>
    </div>
</template>

<style scoped>
.todo {
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
