<script lang="ts">
import { PropType, defineComponent } from "vue"
import {ITodo} from "../interface/ITodo"


export default defineComponent({
    props: {
        todo: {
            type: Object as PropType<ITodo>,
            required: true
        }
    },
    emits: {
        toggleTodo: (id: Number) => Number.isInteger(id),
        deleteTodo: (id: Number) => Number.isInteger(id)
    },
    methods: {
        toggleTodo() {
            this.$emit("toggleTodo", this.todo.id)
        },
        deleteTodo() {
            this.$emit("deleteTodo", this.todo.id)
        }
    }
})

</script>

<template>
    <li class="todo-item" :class="{'todo-item--done' : todo.completed}" @click="toggleTodo">
        <div class="todo-item__status">
            <i class="bi bi-check2"></i>
        </div>
        <span class="todo-item__text">{{ todo.text }}</span>
        <button class="todo-item__remove-button" @click="deleteTodo">
            <i class="bi bi-trash3"></i>
        </button>
    </li>
</template>

<style></style>