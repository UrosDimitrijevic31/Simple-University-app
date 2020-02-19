<template>
  <div class="update">
    <h1>This is an update page</h1>
    <div >
      <div>
      <label v-if="$store.state.isLoggedIn">Your name is: {{name}} </label>
      <input type="text" v-model="computedName" placeholder="Insert new name.." />
      <p>{{name}} {{nameChanged}}</p>
    </div>
    <div>
      <label v-if="$store.state.isLoggedIn">Your surname is: </label>
      <input type="text" v-model="computedSurname" placeholder="Insert new surname.." />
      <p>{{surname}} {{surnameChanged}}</p>
    </div>
      <label v-if="$store.state.isLoggedIn">Your username is: </label>
      <input type="text" v-model="computedUsername" placeholder="Insert new username.." />
      <p>{{username}} {{usernameChanged}}</p>
    </div>
    <div>
      <label v-if="$store.state.isLoggedIn">Your password is not visible: </label>
      <input type="password" v-model="computedPassword" placeholder="Insert new password.." />
      <p>{{password}} {{passwordChanged}}</p>
    </div>
    
    <input type="button" value="submit" @click="update()" />
  </div>
</template>
<script>
import axios from 'axios';
export default {
  components: {},
  data() {
    return {
      username: "",
      password: "",
      name: "",
      surname: "",
      usernameChanged: false,
      passwordChanged: false,
      nameChanged: false,
      surnameChanged: false
    };
  },
  computed: {
    computedUsername: {
      get() {
        //kada iscitava vrednost
        return this.username;
      },
      set(newVal) {
        //kada menjamo vrednost
        this.usernameChanged = true;
        this.username = newVal;
      }
    },
    computedName: {
      get() {
        //kada iscitava vrednost
        return this.name;
      },
      set(newVal) {
        //kada menjamo vrednost, newVal uzima iz inputa
        this.nameChanged = true;
        this.name = newVal;
      }
    },
    computedSurname: {
      get() {
        //kada iscitava vrednost
        return this.surname;
      },
      set(newVal) {
        //kada menjamo vrednost
        this.surnameChanged = true;
        this.surname = newVal;
      }
    },
    computedPassword: {
      get() {
        //kada iscitava vrednost
        return this.password;
      },
      set(newVal) {
        //kada menjamo vrednost
        this.passwordChanged = true;
        this.password = newVal;
      }
    }
  },
  mounted() {},
  methods: {
    update() {
      //potrebno da bi se proverilo da li sesija postoji, da li je ulogovan korisnik
      let params = {
        sid: sessionStorage.getItem("sid")
      };
      if (this.usernameChanged) {
        params.usr_username = this.username;
      }
      if (this.passwordChanged) {
        params.usr_password = this.password;
      }
      if (this.nameChanged) {
        params.usr_name = this.name;
      }
      if (this.surnameChanged) {
        params.usr_surname = this.surname;
      }
      console.log("params", params);

      //komunikacija sa api-jem
       axios.patch('http://044z122.mars-e1.mars-hosting.com/user-api/auth/update', {
        sid: params.sid,
        usr_username: params.usr_username,
        usr_password: params.usr_password,
        usr_name: params.usr_name,
        usr_surname: params.usr_surname
      })
      .then(res => {
        console.log(res.data)
        console.log('korisnik je upisan u bazu', res)
        this.name = res.data.info[0].usr_name;
      })
      .catch(err => {
        console.log(err, 'greska pri abdejtovanju podataka')
      })
      this.username = "",
      this.password = "",
      this.name = "",
      this.surname = ""
    }
    
  }
};
</script>
<style scoped>
div {
  display: block;
}
h1{
  margin-bottom: 40px;
}
div.update{
  margin-top: 5%
}
label{
  display: block;
  font-size: 20px;
}
input[type=text],input[type=password]{
  width: 300px;
  height: 30px;
}
p{
  color: green;
}
</style>
