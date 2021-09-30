<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to"/about">About</router-link>
    </div>
    <router-view/>
    {{ $store.state.count}}
    <Crud />
  </div>
</template>

<script>
import Vue from 'vue'
import router from 'vue-router'
import Crud from './components/Crud.vue'


export default {
  name: 'App',
  components: {
    Crud
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
