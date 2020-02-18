<template>
  <div class="update">
    <h1>This is an update page</h1>
    <div>
      <input type="text" v-model="computedUsername" placeholder="Insert username.." />
      <p>{{username}} {{usernameChanged}}</p>
    </div>
    <div>
      <input type="text" v-model="computedPassword" placeholder="Insert password.." />
      <p>{{password}} {{passwordChanged}}</p>
    </div>
    <div>
      <input type="text" v-model="computedName" placeholder="Insert name.." />
      <p>{{name}} {{nameChanged}}</p>
    </div>
    <div>
      <input type="text" v-model="computedSurname" placeholder="Insert surname.." />
      <p>{{surname}} {{surnameChanged}}</p>
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
      name: "uros",
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
        usr_username: params.usr_username
      })
      .then(res => {
        res
        console.log('korisnik je upisan u bazu', res)
      })
      .catch(err => {
        console.log(err+'greska pri abdejtovanju podataka')
      })
    },
    // sendRequest(){
    //   //staviti url u konstantu
    //   axios.patch('http://044z122.mars-e1.mars-hosting.com/user-api/auth/update', {
    //     params: this.params
    //   })
    //   .then(res => {
    //     console.log('korisnik je upisan u bazu'+res)
    //   })
    //   .catch(err => {
    //     console.log(err)
    //   })    
    // }
  }
};
</script>
<style scoped>
div {
  display: block;
  color: blue;
}
</style>
