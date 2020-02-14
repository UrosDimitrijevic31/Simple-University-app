<template>
  <div class="about">
    <h1>This is an about page</h1>
    <input type="text" v-model="computedIme" placeholder="ime">{{ime}} {{imeChanged}}
    <input type="text" v-model="prezime">{{computedPrezime}}
    <input type="button" value="submit" @click="update()">
  </div>
</template>
<script>
export default {
  components: {

  },
  data(){
    return{
      ime: '',
      prezime: '',
      imeChanged: false,
      prezimeChanged: false
    }
  },
  computed: {
    computedIme: {
      get(){ //kada iscitava vrednost
        return this.ime
      },
      set(newVal){ //kada menjamo vrednost
        this.imeChanged = true;
        this.ime = newVal;
      }
    },
    computedPrezime: {
      get(){ //kada iscitava vrednost
        return this.prezime
      },
      set(newVal){ //kada menjamo vrednost
        this.prezimeChanged = true;
        this.prezime = newVal;
      }
    }
  },
  mounted (){
    

  },
  methods: {
    update (){
      console.log('hello from submit')

      let params = {
        sid: sessionStorage.getItem('sid')
      }
      if(this.imeChanged){
        params.ime = this.ime
      }
      if(this.prezimeChanged){
        params.ime = this.ime
      }
      console.log('params', params)
    }
  }
}
</script>
