<script lang="ts">
import { defineComponent } from 'vue'
import { ITodo } from "./interface/ITodo"
import AppHeader from "./components/AppHeader.vue"
import AppFilters from "./components/AppFilters.vue"
import AppTodoList from "./components/AppTodoList.vue"
import AppAddTodo from "./components/AppAddTodo.vue"
import AppFooter from "./components/AppFooter.vue"

interface State {
  todos: ITodo[],
  filterActive: "All" | "Active" | "Done"
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  data(): State {
    return {
      todos: [
        { id: 0, text: 'Выкинуть мусор', completed: true },
        { id: 1, text: 'Погулять с собакой', completed: false }
      ],
      filterActive: "Active"
    }
  },
  methods: {
    toggleTodo(id: Number) {
      const todo = this.todos.find((todo: ITodo) => todo.id == id)

      if (todo) {
        todo.completed = !todo.completed
      }
    },
    deleteTodo(id: Number) {
      this.todos = this.todos.filter((todo: ITodo) => {
        return todo.id !== id
      })
    },
    addTodo(todo: ITodo) {
      this.todos = [...this.todos, todo]
    },
    setFilter(filter: "All" | "Active" | "Done") {
      this.filterActive = filter
    }
  },
  computed: {
    countDoneTodo() {
      let doneTodo = 0

      for(let i = 0; i < this.todos.length; i++) {
        if(this.todos[i].completed == true) {
          doneTodo += 1
        }
      }

      return doneTodo
    },
    countDoTodo() {
      let doTodo = 0

      for(let i = 0; i < this.todos.length; i++) {
        if(this.todos[i].completed == false) {
          doTodo += 1
        }
      }

      return doTodo
    },
    filterTODO() {
      switch (this.filterActive) {
        case "All":
          return this.todos
        case "Active":
          return this.todos.filter((todo: ITodo) => todo.completed === false)
        case "Done":
        return this.todos.filter((todo: ITodo) => todo.completed === true)
      }
    }
  }
})

</script>

<template>
  <div class="website">
    <AppHeader />

    <AppFilters :active-filter="filterActive" @set-filter="setFilter"/>

    <main class="app-main">

      <AppTodoList :todos="filterTODO" @toggle-todo="toggleTodo" @delete-todo="deleteTodo" />

      <AppAddTodo @add-todo="addTodo" />

    </main>

    <AppFooter :doneTodo="countDoneTodo" :doTodo="countDoTodo" />

  </div>
</template>

<style>

</style>
