<script lang="ts">
import { defineComponent } from "vue"
import { ITodo } from "../interface/ITodo"

interface State {
        isFormVisible: boolean,
        textTodo: string
    }

export default defineComponent({
    data(): State {
        return {
            isFormVisible: false,
            textTodo: ""
        }
    },
    emits: {
        addTodo: (todo: ITodo) => todo
    },
    methods: {
        toggleFormVisible() {
            this.isFormVisible = !this.isFormVisible
        },
        addTodo() {
            this.$emit("addTodo", {
                id: Math.floor(Math.random() * 1000000),
                text: this.textTodo,
                completed: false
            })

            this.textTodo = ""
            this.isFormVisible = false
        }
    }
})
</script>

<template>
    <section class="add-todo">
        <button v-if="!isFormVisible"  @click="toggleFormVisible" class="add-todo__show-form-button">
            <i class="bi bi-plus-lg"></i>
        </button>
        <form v-if="isFormVisible" class="add-todo__form" @submit.prevent="addTodo">
            <button class="close-button"  @click="toggleFormVisible" type="button">
                <i class="bi bi-x"></i>
            </button>
            <div class="text-input text-input--focus">
                <input class="input" v-model="textTodo"/>
            </div>
            <button class="button button--filled">Add task</button>
        </form>
    </section>
</template>

<style></style>