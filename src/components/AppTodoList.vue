<script lang="ts">
import {defineComponent } from 'vue';
import { ITodo } from "@/interface/ITodo"
import AppTodoItem from "./AppTodoItem.vue"

export default defineComponent({
    components: {
        AppTodoItem
    },
    props: {
        todos: Array<ITodo>
    }
})
</script>

<template>
    <ul class="todo-list">
        <AppTodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    </ul>
</template>

<style></style>