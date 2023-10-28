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
    },
    emits: {
        toggleTodo: (id: Number) => Number.isInteger(id),
        deleteTodo: (id: Number) => Number.isInteger(id)
    },
    methods: {
        toggleTodo(id: Number) {
            this.$emit("toggleTodo", id)
        },
        deleteTodo(id: Number) {
            this.$emit("deleteTodo", id)
        }
    }
})
</script>

<template>
    <ul class="todo-list">
        <AppTodoItem v-for="todo in todos" :key="todo.id" :todo="todo" @delete-todo="deleteTodo" @toggle-todo="toggleTodo"/>
    </ul>
</template>

<style></style>