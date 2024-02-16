<script setup lang="ts">
import {Ref, ref} from "vue";

defineProps<{
    todo: TodoItemType
}>()

let editMode: Ref<boolean> = ref(false)

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
    <input type="checkbox" v-model="todo.isSelected" :checked="todo.isSelected">
    <p v-if="!editMode">{{ todo.title }}</p>
    <input v-if="editMode" id="edit-todo" type="text" v-model="todo.title" @focusout="editMode = false"
           @keydown.enter="clickOnSubmitButton(todo)">
    <label v-else for="edit-todo">
        <button @click="clickOnEditButton">Edit</button>
    </label>
    <button v-if="editMode" @click="clickOnSubmitButton(todo)">Submit</button>
</template>

<style scoped></style>
