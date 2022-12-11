<template>
    <header>
        <span v-on:changeWelcome="updateWelcome" v-if="isAuthenticated()">Witaj {{ getUserName() }} </span>
        <router-link to="/"> Home </router-link>
        <router-link v-if="!isAuthenticated()" to="/sign-up">| Sign Up/Login</router-link>
        <a v-if="isAuthenticated()" @click="logout" style="cursor:pointer;"> | Logout</a>
    </header>
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
        this.$router.go();
      },
    }
}

</script>
