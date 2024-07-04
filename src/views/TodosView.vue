<script setup>
  import { ref } from "vue";
  import { uid } from "uid";
  import TodoCreator from '../components/TodoCreator.vue';
  import TodoItem from '../components/TodoItem.vue'

  const todoList = ref([]);
  

  const createTodo = (todo) => {
    todoList.value.push({ 
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null,
    })
  }
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo()" />
    <ul>
      <TodoItem v-for="todo in todoList" v-bind:todo="todo"></TodoItem>
    </ul>
  </main>
</template>  

<style lang="scss" scoped>
  main {
    display: flex;
    flex-direction: column;
    max-width: 580px;
    width: 100%;
    margin: 0 auto;
    padding: 30px 16px;
    h1 {
      margin-bottom: 16px;
      text-align: center;
    }
  }
</style>
