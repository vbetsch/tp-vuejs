<script setup lang="ts">
import {Ref, ref} from "vue";

defineProps<{
    todo: TodoItemType
}>()

const vFocus = {
    mounted: (el: any) => el.focus()
}

let editMode: Ref<boolean> = ref(false)

function clickOnSelectTodo(todo: TodoItemType) {
    todo.isSelected = !todo.isSelected
}

function clickOnEditOrSubmitButton(todo: TodoItemType) {
    if (editMode.value) {
        if (!todo.title) return
    }
    editMode.value = !editMode.value
}
</script>

<template>
    <input type="checkbox" v-model="todo.isSelected">
    <div class="title">
        <input
            v-if="editMode"
            v-focus
            id="edit-todo"
            class="title-input"
            type="text"
            v-model="todo.title"
            @focusout="clickOnEditOrSubmitButton(todo)"
            @keydown.enter="clickOnEditOrSubmitButton(todo)">
        <span v-else class="title-text" @click="clickOnSelectTodo(todo)">{{ todo.title }}</span>
    </div>
    <button @click="clickOnEditOrSubmitButton(todo)">
        {{ editMode ? "Submit" : "Edit" }}
    </button>
</template>

<style scoped>
.title {
    width: 100%;
}

.title-text {
    user-select: none;
}

.title-input {
    width: 12vw;
}
</style>
