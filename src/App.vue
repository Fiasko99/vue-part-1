<template>
  <div id="app">
    <div class="container">
      <h1>Todo application</h1>
      <AddTodo 
        v-on:add-todo="addTodo"
      />
      <hr>
      <TodoList 
        v-bind:todos="todos"
        v-on:remove-todo="removeTodo"
      />
    </div>
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
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(response => response.json())
    .then(json => this.todos = json)
  }
}
</script>

<style scoped>
.container {
  text-align: center;
  width: 70%;
  margin-left: 15%;
}
</style>
