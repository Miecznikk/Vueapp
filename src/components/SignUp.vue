<template>
    <div class="sign_up">
        <form @submit.prevent="sign_up" autocomplete="off">
            <h1>Sign Up</h1>
            <input type="text" v-model="name" placeholder="Enter your name">
            <input type="email" v-model="email" placeholder="Enter your email">
            <input type="password" v-model="password" placeholder="Enter your password">
            <button type="submit">Sign Up</button>
            <span>Have an account? </span><router-link to="/">Log in</router-link>
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
            password:''
        }
    },
    methods: {
        async sign_up(){
            const nameIsValid = this.name!='';
            const passwordIsValid = this.password.length > 7;
            const formValid = nameIsValid && passwordIsValid;
            let users = await axios.get(`http://localhost:3000/users?email=${this.email}`);
            if(users.status == 200 || users.status == 304){
                users = users.data;
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
            else{
                alert("Something went wrong")
            }
        }
    },
}
</script>
<style>

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