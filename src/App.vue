<template>
  <div id="app">
      <NavBar @changeWelcome="updateWelcome"/>
      <router-view :key="$route.fullPath"/>
    </div>
</template>

<script>
  //
  import NavBar from './components/NavBar.vue'
  export default {
    data(){
      return {
        
      }
    },
    components:{
      NavBar
    },
    methods:{
      updateWelcome(){
        console.log('3')
      }
    },
  }
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body{
  padding: 0;
  margin: 0;
}

</style>
