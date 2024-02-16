<script setup lang="ts">
import {reactive, Ref, ref} from "vue";
import Todo from "./TodoItem.vue";

let todos: TodoItemType[] = reactive([])
let displayedTodos: TodoItemType[] = reactive([])
let inputNewValue: Ref<string> = ref("")
let searchValue: Ref<string> = ref("")
let searchMode: Ref<boolean> = ref(false)

function clickOnAddTodo() {
    if (inputNewValue.value) {
        todos.push({
            title: inputNewValue.value,
            isSelected: false,
            isDone: false
        })
        inputNewValue.value = ""
    }
}

function clickOnDeleteSelectedTodos() {
    const selectedTodos = todos.filter((todo: TodoItemType) => todo.isSelected)
    selectedTodos.map((todo: TodoItemType) => clickOnDeleteTodo(todo))
}

function clickOnDeleteTodo(todo: TodoItemType) {
    todos.splice(
        todos.indexOf(todo),
        1
    );
}

function onKeyUpSearchBar() {
    searchMode.value = true;
    displayedTodos = todos.filter((todo) => (
        todo.title.includes(searchValue.value)
    ))
}

</script>

<template>
    <input
        id="new-todo"
        type="text"
        placeholder="Add a new todo"
        v-model="inputNewValue"
        @keydown.enter="clickOnAddTodo"
        autofocus
    >
    <label for="new-todo">
        <button @click="clickOnAddTodo">Add</button>
    </label>
    <button @click="clickOnDeleteSelectedTodos">Delete selected</button>
    <div class="filter">
        <input
            id="search-bar"
            type="text"
            placeholder="Search a todo..."
            v-model="searchValue"
            @keyup="onKeyUpSearchBar"
            @focusout="searchMode = false"
        >
    </div>
    <div v-if="searchMode" class="todolist">
        <div v-for="todo in displayedTodos" :key="todos.indexOf(todo)"
             :class="'todo' + (todo.isDone ? ' done' : '') + (todo.isSelected ? ' selected' : '')">
            <Todo :todo="todo" :function-to-delete-todo="clickOnDeleteTodo"/>
        </div>
        <p v-if="!displayedTodos.length">No todo found</p>
    </div>
    <div v-else class="todolist">
        <div v-for="todo in todos" :key="todos.indexOf(todo)"
             :class="'todo' + (todo.isDone ? ' done' : '') + (todo.isSelected ? ' selected' : '')">
            <Todo :todo="todo" :function-to-delete-todo="clickOnDeleteTodo"/>
        </div>
    </div>
</template>

<style scoped>
.todolist {
    display: flex;
    width: 100%;
    flex-direction: column;
    padding: 10px;
    gap: 10px;
}

.todo {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #424242;
    padding: 10px 20px;
    border-radius: 10px;
}

.todo.done {
    background-color: #00cc86;
}

.todo.selected {
    background-color: #646cff;
}
</style>
