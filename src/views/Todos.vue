<template>
  <div>
    <h2>Todo application</h2>

    <router-link to="/">Home</router-link>

    <AddTodo 
    v-on:add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr>
    <transition name="slide-fade" mode="out-in">
      <Loader 
        v-if="loading"
      />
      <TodoList 
        v-else-if="!loading"
        v-bind:todos="filteredTodos"
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
      loading: true,
      filter: 'all'
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
  },
  computed: {
    filteredTodos() {
      if(this.filter === 'all') {
        return this.todos
      } else if(this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      } else if(this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
    }
  }
}
</script>

<style scoped>

</style>