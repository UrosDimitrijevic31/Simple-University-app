<template>
  <div class="bla">
      <div v-if="!isLoggedIn">
        <h1>Login</h1>
        <label for="emial">Email</label>
        <input type="email" placeholder="Insert email.." v-model="email">
        <label for="password">Insert password</label>
        <input type="password" placeholder="Insert password.." v-model="password">
        <button @click="login()">LogIn</button>
      </div>
      <div v-if="isLoggedIn">
          <h1>You are LoggedIn</h1>
        <button  @click="logout()">LogOut</button>
      </div>
      {{email}}
  </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return{
            email: null,
            password: null,
            isLoggedIn: false,
            user: []
        }
    },
    methods: {
        login(){
            axios.post('http://044z122.mars-e1.mars-hosting.com/user-api/auth/login', {
                email: this.email,
                password: this.password
            })
            .then(res => {
                console.log(res.data)
                console.log('usepsno logovanje')
                //sacuvali smo sid u localstorage-u, objekat sesije, sa njim sve radimo
                sessionStorage.setItem('sid', res.data.sid);

                this.isLoggedIn = true;

                this.user = sessionStorage.getItem('user');
                console.log('ovo je getItem',sessionStorage.getItem('user'))
               
            }).catch(err => {
                console.log(err);
                console.log('pogresno uneti email ili pass')
            })
            //treba da resetoju vrednosti, ali moram da pogledam kako se ponasa zbog sesije
            // this.email = null,
            // this.password = null
        },
        logout(){
            axios.post('http://044z122.mars-e1.mars-hosting.com/user-api/auth/logout'), {         

            }
            .then(res => {
                console.log(res.data)
                console.log('usepsno logout')
                this.isLogin = false;
                //sacuvali smo sid u localstorage-u, objekat sesije
         
            }).catch(err => {
                console.log(err);
                console.log('nesto ne valja')
            })
            //treba da resetoju vrednosti, ali moram da pogledam kako se ponasa zbog sesije
            // this.email = null,
            // this.password = null
        }
    }
}
</script>

<style scoped>
input[type=email], input[type=password] {
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
  background-color: #4CAF50;
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
  width: 20%;
  margin-left: 40%;
} 
</style>

