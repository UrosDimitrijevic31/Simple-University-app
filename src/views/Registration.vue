<template>
<div>
  <div class="bla" v-if="!isRegistrated">
    <h1>Registration</h1>
    <div>
      <!--napraviti da je neophodno ineti podatke-->
      <label for="fname">Username</label>
      <input type="text" placeholder="Insert username.." v-model="username" />
      <label for="fname">First Name</label>
      <input type="text" placeholder="Insert name.." v-model="name" />
      <label for="lname">Last Name</label>
      <input type="text" placeholder="Insert lastanem.." v-model="surname" />
      <label for="email">E-mail</label>
      <input type="text" placeholder="Insert email.." v-model="email" />
      <label for="password">Password</label>
      <input type="password" placeholder="Insert password.." v-model="password" />
    </div>
    <div v-if="isAdmin">  
      <input type="radio" name="rola" >Admin
      <input type="radio" name="rola" >User
    </div>
      <button @click="registration()">Registration</button>

  </div>
      <div v-if="isRegistrated">
        <p>You are successfully registered </p> 
      </div>
  </div>
  
</template>
    
<script>
import axios from "axios";
export default {
  data() {
    return {
      username: null,
      name: null,
      surname: null,
      email: null,
      password: null,
      isRegistrated: false,
      isAdmin: false,
      rolName: ''

    };
  },
  methods: {
    registration() {
      axios
        .post("http://044z122.mars-e1.mars-hosting.com/user-api/auth/signup", {
          username: this.username,
          name: this.name,
          surname: this.surname,
          email: this.email,
          password: this.password
        })
        .then(resp => {
          console.log(resp);
          console.log("uspesna registracija");
          this.isRegistrated = true;
          
        })
        .catch(err => {
          console.log(err);   
          console.log('neuspesna registarcija')
        });
    },
  }
};
</script>

<style scoped>
input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

button {
  width: 100%;
  background-color: #4caf50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.bla {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
  width: 50%;
  margin-left: 25%;
}
</style>>

