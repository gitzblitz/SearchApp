<template>
  <div class="container">
    <img class="center-block" src="./assets/logo.png">
      <search></search>

  </div>
</template>

<script>
import Search from '@/components/Search'

export default {
  components: {Search},
  name: 'app',
  data () {
    return {
      msg: 'Hello Search'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
