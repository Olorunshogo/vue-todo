<script setup>
  import { RouterView } from 'vue-router'
  import TodoHeader from './components/TodoHeader.vue'
  import TodosView from './views/TodosView.vue';
</script>

<template>
  <TodoHeader />
  

  <RouterView />
  <TodosView></TodosView>
</template>

<style lang="scss">

</style>
