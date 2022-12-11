<template>
    <div class="login">
        <form @submit.prevent="login" autocomplete="off">
            <h1>Log In</h1>
            <input type="email" v-model="email" placeholder="Enter your email">
            <input type="password" v-model="password" placeholder="Enter your password">
            <button type="submit">Log In</button>
            <span class="text-red" v-if="!formIsValid">Invalid email or password</span>
        </form>
    </div>
</template>
<script>
import axios from 'axios'

export default {
    name:'LogIn',
    data(){
        return {
            email:'',
            password:'',
            formIsValid:true
        }
    },
    methods: {
        async login(){
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`);
            if(result.status === 200 || result.status === 304){
                if(result.data.length == 1){
                    this.formIsValid = true;
                    console.log(result.data[0].name);
                    localStorage.setItem('authenticated',"1");
                    localStorage.setItem('email',this.email);
                    localStorage.setItem('name',result.data[0].name);
                    this.$router.go('/');
                }
                else{
                    this.formIsValid = false;
                }
            }
        }
    },
    mounted() {
        if(localStorage.getItem('authenticated') == 1){
            this.$router.push('/')
        }
    },
}
</script>
<style>
    
</style>
