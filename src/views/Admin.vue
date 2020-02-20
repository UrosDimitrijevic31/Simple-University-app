<template>
  <div v-if="$store.state.isAdmin">
    <h1>Hello Admin</h1>

    <button @click="users()">Get all users</button>
    <ol class="lista">
      <li v-for="(user, index) in info" :key="index" @click="editUser(user.usr_id)">{{user.usr_name}} {{user.usr_surname}}</li>
    </ol>

    <input type="text" placeholder="insert email..." v-model="email" />
    <button @click="findUser">Find User</button>
    <div v-for="(user, index) in singleUser" :key="index">{{user.usr_name}} {{user.usr_surname}}</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      info: [],
      email: null,
      singleUser: []
    };
  },
  methods: {
    users() {
      axios
        .get("http://044z122.mars-e1.mars-hosting.com/user-api")
        .then(response => {
          console.log(response.data);
          this.info = response.data;
        });
    },

    findUser() {
      axios
        .get(
          "http://044z122.mars-e1.mars-hosting.com/user-api?email=" + this.email
        )
        .then(response => {
          console.log(response.data);
          this.singleUser = response.data.data;
        });
    },
    // editUser(){
    //     axios.patch('http://044z122.mars-e1.mars-hosting.com/user-api/auth/users-edit', {
    //         sid: sessionStorage.getItem("sid")
    //     })
    //     .then(res => {
    //         res
    //         console.log('uspesno prosao request')
    //     })
    //     .catch(err => {
    //         err
    //         console.log('nije prosao request')
    //     })
    // },
    editUser(id) {
        this.$router.push({
            name:'updateUser',
            params: {
                id
            }
        })
    }
  }
};
</script>

<style>
.lista {
  width: 20%;
  margin-left: 40%;
  list-style: none;
}
li{
    /* margin: 5px; */    
}
li:hover {
  /* box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5); */
  border-bottom: 2px solid #9999ff;

}
</style>