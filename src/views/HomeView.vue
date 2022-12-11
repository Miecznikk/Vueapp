<template>
  <div class="home">
    <h1>Welcome to our restaurant page</h1>
    <h2>These are restaurants in our region</h2>
    <table>
      <thead>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">Address</th>
          <th scope="col">Contact</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,i) in restaurants" :key="i">
          <th scope="row">{{ item.name }}</th>
          <th scope="row">{{ item.address }}</th>
          <th scope="row">{{ spaceNumber(item.contact) }}</th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name:'HomeView',
    data(){
      return {
        restaurants:[]
      }
    },
    async mounted() {
      let result = await axios.get('http://localhost:3000/restaurants');
      this.restaurants = result.data;
    },
    methods:{
      spaceNumber(numb){
        return numb.toLocaleString();
      }
    }
  }
</script>
<style>
  table{
    margin:0 auto;
    font-size:1.3rem;
  }
  th{
    width:160px;
    height:40px;
  }
  thead{
    background-color:skyblue ;
  }
  tbody{
    background-color:#f2f2f2;
    color:#333
  }
</style>