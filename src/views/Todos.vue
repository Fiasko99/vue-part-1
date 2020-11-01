<template>
  <div>
    <h2>Todo application</h2>

    <router-link to="/">Home</router-link>

    <AddTodo 
    v-on:add-todo="addTodo"
    />
    <hr>
    <transition name="slide-fade" mode="out-in">
      <Loader 
        v-if="loading"
      />
      <TodoList 
        v-else-if="!loading"
        v-bind:todos="todos"
        v-on:remove-todo="removeTodo"
      />
    </transition>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return {
      todos:[],
      loading: true
    }
  },
  components: {
    TodoList, AddTodo, Loader
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    },
    async updateData() {
      await fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(json => this.todos = json)
    }
  },
  mounted() {
    setTimeout(() => {
      this.updateData()
      this.loading = false
    }, 1500)
  }
}
</script>

<style scoped>

</style>