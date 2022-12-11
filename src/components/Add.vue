<template>
    <div class='add'>
        <form @submit.prevent="addRestaurant">
            <h2>Add restaurant</h2>
            <input v-model="Restaurant.name" type="text" name="name" placeholder="Enter restaurant's name" autocomplete="off">
            <p class="text-red" v-if="!Restaurant.nameIsValid">Name invalid</p>
            <input v-model="Restaurant.address" type="text" name="address" placeholder="Enter restaurant's address" autocomplete="off">
            <p class="text-red" v-if="!Restaurant.addressIsValid">Adress invalid</p>
            <input v-model="Restaurant.contact" type="text" name="contact" placeholder="Enter restaurant's contact" autocomplete="off">
            <p class="text-red" v-if="!Restaurant.contactIsValid">Contact number invalid</p>
            <button type="submit">Submit</button>
        </form>
    </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'

export default {
    name:'Add',
    data(){
        return {
            Restaurant:{
                name:'',
                address:'',
                contact:'',
                nameIsValid: true,
                addressIsValid: true,
                contactIsValid: true
            }
        }
    },
    mounted() {
        if(localStorage.getItem('authenticated')!="1"){
            this.$router.push('/login');
        }
    },
    methods: {
        async addRestaurant(){
            this.Restaurant.nameIsValid = this.Restaurant.name != '';
            this.Restaurant.addressIsValid = this.Restaurant.address != '';
            this.Restaurant.contactIsValid = 7 <= this.Restaurant.contact.length && this.Restaurant.contact.length <= 9 && /^\d+$/.test(this.Restaurant.contact)

            const formIsValid = this.Restaurant.nameIsValid && this.Restaurant.contactIsValid && this.Restaurant.addressIsValid;

            if(formIsValid){
                let result = await axios.post("http://localhost:3000/restaurants",{
                    name:this.Restaurant.name,
                    address:this.Restaurant.address,
                    contact:parseInt(this.Restaurant.contact)
                });
                if (result.status == 201){
                    alert('Succesfully added a restaurant!');
                    this.$router.go();
                }
                else{
                    alert('Something went wrong contacting with server');
                    this.$router.push('/')
                }
            }
            
            
            
        }
    },
}
</script>
<style>

</style>