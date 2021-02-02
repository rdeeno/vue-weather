<template>
  <div id="app">
    <Page />
  </div>
</template>

<script>
import Page from '@/components/Page.vue'

export default {
  name: 'App',
  components: {
    Page
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
}
#app {
  font-family: 'Poppins', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
