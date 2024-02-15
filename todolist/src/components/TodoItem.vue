<script setup lang="ts">
import {ref} from "vue";

defineProps<{
    todo: TodoItemType
}>()

let editMode = ref(false)
</script>

<template>
    <p v-if="!editMode">{{ todo.title }}</p>
    <input v-if="editMode" id="edit-todo" type="text" v-model="todo.title">
    <label v-else for="edit-todo">
        <button @click="editMode = true">Edit</button>
    </label>
    <button v-if="editMode" @click="editMode = false">Submit</button>
</template>

<style scoped>

</style>
