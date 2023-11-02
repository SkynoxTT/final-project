<template>
  <div class="container">
    <NavComp/>
    <router-view></router-view>
  </div>
</template>

<script>

import NavComp from './components/Navigation.vue'

export default {
  name: 'App',
  components: {
    NavComp
  }
}
</script>

<style>
.container{
  background-color: gray;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}
</style>
