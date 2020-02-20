<template>
  <div class="bla">
      <div v-if="!$store.state.isLoggedIn">
        <h1>Login</h1>
        <label for="emial">Insert email</label>
        <input type="email" placeholder="Insert email.." v-model="email">
        <label for="password">Insert password</label>
        <input type="password" placeholder="Insert password.." v-model="password">
        <button @click="login()">LogIn</button>
      </div>
      <div v-if="$store.state.isLoggedIn">
        <h1>Hello, {{username}}</h1>   
        <button @click="logout()">LogOut</button>
      </div>

      <div v-if="$store.state.isAdmin">
        cao admine    
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
            rolName: '',
            username: null
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
                this.$store.state.isLoggedIn = true;
                this.rolName = res.data.rolaName;
                this.username = res.data.username;
                console.log('naziv role je',res.data.rolaName)
             
                console.log('ovo je iz vuexa isLogedIn ', this.$store.state.isLoggedIn)


                if(this.rolName === 'admin'){
                  this.$store.state.isAdmin = true;
                }
                console.log('ovo je iz vuexa isAdmin ', this.$store.state.isAdmin)
               
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
                this.$store.state.isLoggedIn = false;
                sessionStorage.removeItem('sid');
                sessionStorage.removeItem('user');
                console.log('usepsno logout')
                this.$store.state.isAdmin = false;
                // console.log('da li je admin',this.isAdmin)
                console.log('ovo je iz vuexa isAdmin ', this.$store.state.isAdmin)
                console.log('ovo je iz vuexa isLogedIn ', this.$store.state.isLoggedIn)
                this.rolName = '';
            }).catch(err => {
                console.log('nesto ne valja', err)
            })
            this.email = null,
            this.password = null,
            this.username = null,
            this.$store.state.isLoggedIn = false;
        }
    }
}
</script>

<style scoped>
h1{
  margin-bottom: 35px;
}

input[type=email], input[type=password] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-bottom: 15px;
}
label {
  font-weight: bold;
}
button {
  width: 40%;
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
  padding: 20px;
  width: 20%;
  margin-left: 40%;
} 
</style>

