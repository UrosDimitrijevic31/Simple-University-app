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
        <button @click="logout()">LogOut</button>
      </div>
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
                sessionStorage.setItem('user', res.data.user); //prosledio sam id
                //treba nam da znamo da li je user ulogovan, nije dobro da stoji ovde        
                this.isLoggedIn = true;
               
            }).catch(err => {
                console.log(err);
                console.log('pogresno uneti email ili pass')
            })


        },
        //mars sam zna sta da uradi kad mu posaljemo sid, treba samo da ga posaljemo
        logout(){
            axios.post('http://044z122.mars-e1.mars-hosting.com/user-api/auth/logout', {         
                sid: sessionStorage.getItem('sid')
            })
            .then(res => {
                console.log(res.data)
                this.isLogin = false;
                sessionStorage.removeItem('sid');
                sessionStorage.removeItem('user');
                console.log('usepsno logout')
            }).catch(err => {
                console.log(err);
                console.log('nesto ne valja')
            })
            
            this.isLoggedIn = false;
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

