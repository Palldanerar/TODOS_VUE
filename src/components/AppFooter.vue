<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    props: {
        doTodo: Number,
        doneTodo: Number
    }
})
</script>

<template>
    <footer class="app-footer">{{ doTodo }} more to do, {{ doneTodo }} done</footer>
</template>

<style></style>