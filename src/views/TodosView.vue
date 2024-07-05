<script setup>
  import { ref, watch, computed } from "vue";
  import { uid } from "uid";
  import { Icon } from '@iconify/vue'

  import TodoCreator from '../components/TodoCreator.vue';
  import TodoItem from '../components/TodoItem.vue'

  const todoList = ref([]); 

  // This accepts a few parameters like the reactive data that we want to watch
  watch(todoList, () => {
    setTodoListLocalStorage();
   }, {
      deep: true,
  });

  // Display a message after every todo is checked.
  const todoCompleted = computed(() => {
    return todoList.value.every((todo) => todo.isCompleted);
  });

  const fetchTodoList = () => {
    // We need to parse the item (savedTodoList) we got from local storage.
    const savedTodoList = JSON.parse(localStorage.getItem("todoList") );
    if (savedTodoList) {
      todoList.value = savedTodoList;
    }
  };
  fetchTodoList();
  
  // A re-usable function to save the reusable function to local storage. It'll also be executed each time a todo is created or updated.
  const setTodoListLocalStorage = () => {
    // setItem() is how we set an item to local storage. It accepts 2 par: key and value.
    // Key will be a string and is basically the name of the item being set to the local storage.
    // The value must also be a string. So, we stringify our todoList.
    localStorage.setItem("todoList", JSON.stringify(todoList.value) );
  };  

  const createTodo = (todo) => {
    todoList.value.push({ 
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null,
    });
    // setTodoListLocalStorage();
  };

  const toggleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
    // setTodoListLocalStorage();
  };

  const toggleEditTodo = (todoPos) => {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
    // setTodoListLocalStorage();
  };

  const updateTodo = (todoVal, todoPos) => {
    todoList.value[todoPos].todo = todoVal;
    // setTodoListLocalStorage();
  };

  const deleteTodo = (todoId) => {
    todoList.value = todoList.value.filter((todo) => todo.id != todoId);
    // setTodoListLocalStorage();
  };
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
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        >
        </TodoItem>
      </ul>
      <p class="todosMsg" v-else>
        <Icon icon="emojione-v1:sad-but-relieved-face" width="1.5rem" />
        <span>You have no todos to complete! Add one!</span>
      </p>
      <p v-if="todoCompleted && todoList.length" class="todosMsg">
        <span>You have completed all your todos.</span>
        <Icon icon="noto:party-popper" width="2.5rem" />
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
