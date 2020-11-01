<template>
  <div>
    <h2>Todo application</h2>

    <router-link to="/">Home</router-link>

    <AddTodo 
    v-on:add-todo="addTodo"
    />
    <hr>
    <TodoList 
    v-bind:todos="todos"
    v-on:remove-todo="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'

export default {
  name: 'App',
  data() {
    return {
      todos:[]
    }
  },
  components: {
    TodoList, AddTodo
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
    this.updateData()
  }
}
</script>

<style scoped>

</style>