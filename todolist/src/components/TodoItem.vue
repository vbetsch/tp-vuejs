<script setup lang="ts">
import {Ref, ref} from "vue";

defineProps<{
    todo: TodoItemType
    functionToDeleteTodo: (todo: TodoItemType) => void
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
            placeholder="Edit todo title"
            @keydown.enter="clickOnEditOrSubmitButton(todo)"
        >
        <span v-else class="title-text" @click="clickOnSelectTodo(todo)">{{ todo.title }}</span>
    </div>
    <div class="buttons">
        <button class="button" @click="todo.isDone = !todo.isDone">
            {{ todo.isDone ? "Cancel" : "Done" }}
        </button>
        <button class="button" @click="clickOnEditOrSubmitButton(todo)">
            {{ editMode ? "Submit" : "Edit" }}
        </button>
        <button class="button" @click="functionToDeleteTodo(todo)">Delete</button>
    </div>
</template>

<style scoped>
.title {
    width: 12vw;
    overflow: hidden;
    text-overflow: ellipsis;
}

.title-text {
    user-select: none;
}
.buttons {
    display: flex;
    gap: 5px;
}
.button {
    width: 100px;
}
</style>
