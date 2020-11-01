<template>
  <li>
      <span v-bind:class="{done: todo.completed}">
          <input type="checkbox" v-on:change="todo.completed = !todo.completed">
          <strong>{{index + 1}}</strong>
          {{todo.title}}
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
    }
}
</script>

<style scoped>
 li {
     border: 1px solid #ccc;
     display: flex;
     justify-content: space-between;
     padding: 0.5rem 2rem;
     margin: 1rem;
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