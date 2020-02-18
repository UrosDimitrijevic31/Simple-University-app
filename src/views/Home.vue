<template>
  <div class="home">
    <HelloWorld msg="Welcome to Simple User Interface"/>

      <button @click="users()">Get all users</button> 
      <div v-for="(user, index) in info" :key="index">
        {{user.usr_name}} || {{user.usr_surname}}
      </div>

      <input type="text" placeholder="insert email..." v-model="email">
      <button @click="findUser">Find User</button>
      <div v-for="(user, index) in singleUser" :key="index">
        {{user.usr_name}} {{user.usr_surname}}
      </div>
      <button @click="checkSession()">check session</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  // mounted(){
  // this.users();
  // },
  data(){
    return {
      info: [],
      email: null,
      singleUser: []
    }
  },
  methods: {
    users() {
      axios.get('http://044z122.mars-e1.mars-hosting.com/user-api')
      .then(response => {
        console.log(response.data);      
        this.info = response.data;
      })  
    },
    findUser(){
      axios.get('http://044z122.mars-e1.mars-hosting.com/user-api?email='+this.email)
      .then(response => {
          console.log(response.data);
          this.singleUser = response.data.data
      })
    },
    //provera da li je setovana sesija
    checkSession(){
      axios.post('http://044z122.mars-e1.mars-hosting.com/user-api/auth/checkSession', {
        //kako da posaljemo sesiju sa fronta
      })
      .then(response => {
          console.log(response);
          console.log('sesija postoji')
      }).catch(err => {
        console.log('sesija ne postoji')
        console.log(err);
        })
    }
  }  
}
</script>

<style scoped>
.home{
  width:40%;
  margin-left: 30%; 
}
  input, button{
    display: block;
    color: green;
    margin: 5px;
  }
</style>
