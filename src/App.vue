<template>
  <div id="app">
    <HeaderApp />
    <TodoApp />
  </div>
</template>



<script>
  import HeaderApp from './components/HeaderApp.vue'
  import TodoApp from './components/TodoApp.vue'


  export default {
    name: 'App',
    components: {
      HeaderApp,
      TodoApp,
    }
  }
</script>
