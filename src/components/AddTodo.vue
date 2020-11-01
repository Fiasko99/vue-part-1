<template>
  <form v-on:click.prevent="onSubmit">
      <input type="text" v-model="title">
      <button type="submit">Create</button>
  </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }

                this.$emit('add-todo', newTodo)
                this.title = ''
            }
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
        margin: 0.5rem;
        padding: 1rem;
        border: 2px solid #888;
        border-radius: 4px;
    }
    input {
        width: 100%;
        margin-right: 1rem;
        border-radius: 4px;
        border: 1px solid #666;
    }
    input:focus {
        outline: none;
    }
</style>