<script setup lang="ts">
import {ref} from "vue";

defineProps<{
    todo: TodoItemType
}>()

let editMode = ref(false)

function clickOnEditButton() {
    editMode.value = true
}

function clickOnSubmitButton(todo: TodoItemType) {
    if (todo.title !== "") {
        editMode.value = false
    }
}
</script>

<template>
    <p v-if="!editMode">{{ todo.title }}</p>
    <input v-if="editMode" id="edit-todo" type="text" v-model="todo.title" @focusout="editMode = false"
           @keydown.enter="clickOnSubmitButton(todo)">
    <label v-else for="edit-todo">
        <button @click="clickOnEditButton">Edit</button>
    </label>
    <button v-if="editMode" @click="clickOnSubmitButton(todo)">Submit</button>
</template>

<style scoped></style>
