<script setup>
  import { ref } from "vue";
  import { uid } from "uid";
  import { Icon } from '@iconify/vue'

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
  };
  const toggleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
  }

  const toggleEditTodo = (todoPos) => {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
  };

  const updateTodo = (todoPos, todoVal) => {
    todoList.value[todoPos.todo] = todoVal;
  }
</script>

<template>
  <div class="container">
    <main>
      <h1>Create Todo</h1>
      <TodoCreator @create-todo="createTodo($event)" />
      <ul class="todoList" v-if="todoList.length">
        <TodoItem 
          v-for="(todo, index) in todoList" 
          v-bind:key="todo" v-bind:todo="todo" v-bind:index="index" 
          @toggleComplete="toggleTodoComplete"
          @edit-todo="toggleEditTodo"
          @update-todo="updateTodo">
        </TodoItem>
      </ul>
      <p class="todosMsg" v-else>
        <Icon icon="emojione-v1:sad-but-relieved-face" />
        <Icon icon="emojione-v1:sad-but-relieved-face" />
        <span>You have no todo's to complete! Add one!</span>
      </p>
    </main>
  </div>
</template>  

<style lang="scss" scoped>
  .container {
    max-width: 1100px;
    margin: 0 auto;
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

      .todoList {
        display: flex;
        flex-direction: column;
        list-style-type: none;
        margin-top: 24px;
        gap: 20px;
      }

      .todosMsg {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        gap: 8px;
        margin-top: 24px;
      }
    }
  }
  
</style>
