<template>
  <li>
      <span v-bind:class="{done: todo.completed}" class="todo-title" :data="todo.title">
          <input type="checkbox" v-on:change="todo.completed = !todo.completed">
          <strong>{{index + 1}}</strong>
          {{todo.title | uppercase}}
      </span>
      <button 
        class="rm" 
        v-on:click="$emit('remove-todo', todo.id)"
      >&times;</button>
  </li>

</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    },
    filters: {
      uppercase (value) {
        return value.toUpperCase()
      }
    }
}
</script>

<style scoped>
 li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 1.5rem;
    margin: 1rem;
    position: relative;
 }
 .todo-title {
    width: 70% !important;
    overflow-x: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    text-align: left;
 }
 .todo-title:hover::after {
    content: attr(data);
    position: absolute;
    left: 3rem;
    top: 3rem;
    min-width: 200px;
    border: 1px #ccc solid;
    background-color: #ffffcc;
    padding: 0.5rem 1.5rem;
    color: #000000;
    font-size: 14px;
    z-index: 1;
 }
 .rm {
     background: #ccc;
     color: #fff;
     border-radius: 50%;
     font-weight: bolder;
     cursor: pointer;
 }
 .rm:focus {
     outline: none;
 }
 .done {
     text-decoration: line-through;
 }
 input {
     margin-right: 1rem;
 }
</style>