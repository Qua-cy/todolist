<template>
  <div>
    <main-header></main-header>
    <main-todo></main-todo>
    <main-footer></main-footer>
  </div>
</template>

<script>
import './assets/css/global.css'

import MainHeader from './components/MainHeader.vue'
import MainTodo from './components/MainTodo/MainTodo.vue'
import MainFooter from './components/MainFooter.vue'
export default {
  name: 'App',
  components:{
     MainHeader,
     MainTodo,
     MainFooter
  }
}
</script>

<style>
  
</style>
