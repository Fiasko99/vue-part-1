<template>
  <div>
    <transition name="slide-fade" mode="out-in">
      <transition-group name="slide-fade" mode="ease" tag="ul" v-if="todos.length">
            <TodoItem 
                v-for="(todo, index) in todos"
                v-bind:todo="todo"
                v-bind:key="todo.id"
                v-on:remove-todo="removeTodo"
                v-bind:index="index"
            />
      </transition-group>
      <p v-else-if="!todos.length">No todos!</p>
    </transition>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'

export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeTodo (id) {
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style scoped>
ul {
    list-style: none;
    margin: 0;
    padding: 0;
}
</style>