<template>
  <div id="app">
    <header>Minhas Tarefas</header>
    <TaskVue/>
  </div>
</template>
<script>
import TaskVue from './components/Task.vue'
  export default { 
    name : 'App',
    components:{ 
      TaskVue
    }
  }
</script>

<style scoped>
 header {
   display: flex;
   justify-content: center;
   align-items: center;
   width: 100%;
   height: 80px;
   font-size: 40px;
   color: #FFF;
 }
</style>