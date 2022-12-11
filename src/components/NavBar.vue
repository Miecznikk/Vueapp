<template>
    <div class="nav">
        <router-link to="/"> Home </router-link>
        <router-link v-if="!isAuthenticated()" to="/sign-up"> Sign Up/Login</router-link>
        <router-link v-if="isAuthenticated()" to="/add">Add restaurant</router-link>
        <router-link v-if="isAuthenticated()" to="/update">Update restaurant</router-link>
        <a v-if="isAuthenticated()" @click="logout" style="cursor:pointer;"> Logout</a>
    </div>
</template>

<script>

export default{
    name:'NavBar',
    methods:{
      getUserName(){
        return localStorage.getItem('name');
      },
      isAuthenticated(){
        return localStorage.getItem('authenticated') == "1";
      },
      logout(){
        localStorage.clear();
        this.$router.go('/login');
      },
    }
}

</script>

<style>

.nav{
  background-color: #333;
  overflow: hidden;
}

.nav *{
  float:left;
  color:#f2f2f2;
  padding:16px 14px;
  text-align: center;
}

.nav *:hover{
  background-color:#ddd;
  color:#333;
}

</style>