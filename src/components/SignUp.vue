<template>
    <div class="sign_up">
        <form @submit.prevent="sign_up" autocomplete="off">
            <h1>Sign Up</h1>
            <input type="text" v-model="name" placeholder="Enter your username">
            <span class="text-red" v-if="!nameIsValid">Invalid username</span>
            <input type="email" v-model="email" placeholder="Enter your email">
            <span class="text-red" v-if="!emailIsValid">Email invalid</span>
            <input type="password" v-model="password" placeholder="Enter your password">
            <span class="text-red" v-if="!passwordIsValid">Invalid password</span>
            <button type="submit">Sign Up</button>
            <span>Have an account? </span><router-link to="/login">Log in</router-link>
        </form>
    </div>
</template>
<script>
/* eslint-disable */
import axios from 'axios';
export default {

    name: 'SignUp',
    data(){
        return{
            name:'',
            email:'',
            password:'',
            nameIsValid:true,
            emailIsValid:true,
            passwordIsValid:true
        }
    },
    methods: {
        async sign_up(){
            this.nameIsValid = this.name.length > 4;
            this.passwordIsValid = this.password.length > 7;
            this.emailIsValid = this.email.length > 4;
            const formValid = this.nameIsValid && this.passwordIsValid;
            if(formValid){
                let users = await axios.get(`http://localhost:3000/users?email=${this.email}`);
                if(users.status == 200 || users.status == 304){
                    users = users.data;
                    console.log(users[0]);
                    if(users.length>0){
                        this.emailIsValid = false;
                        alert('Email already taken!')
                        return;
                    }
                }
            }
            if(formValid){
                console.log('success')
                let result = await axios.post("http://localhost:3000/users",{
                    name: this.name,
                    email: this.email,
                    password: this.password
                })
                if(result.status === 201){
                    alert("Sign Up Success!")
                    this.name='';
                    this.email='';
                    this.password='';
                    this.$router.push('/')
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
    .text-red{
        color:rgb(211, 0, 0);
    }

    form input{
        display:block;
        margin:10px auto;
        width:300px;
        height:40px;
        padding-left: 20px;
        border: 1px solid skyblue;
        border-radius: 4px;
        
    }
    form button{
        display:block;
        margin: 10px auto;
        width:320px;
        height:40px;
        background-color: skyblue;
        border:1px solid rgb(44, 185, 255);
        color:white;
        border-radius: 5px;
        transition: background-color 0.2s ease-out;
    }
    form button:hover{
        background-color:rgb(86, 86, 255);
    }
    a{
        text-decoration: none;
        color:rgb(0, 86, 206);
    }
</style>