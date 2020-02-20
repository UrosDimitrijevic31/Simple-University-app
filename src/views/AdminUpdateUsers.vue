<template>
  <div class="update">
    <h1>ovo je strana za update profila usera</h1>
    <div>
      <div>
        <label v-if="$store.state.isLoggedIn">Your name is: {{name}}</label>
        <input type="text" v-model="computedName" placeholder="Insert new name.." />
        <p>{{name}} {{nameChanged}}</p>
      </div>
      <div>
        <label v-if="$store.state.isLoggedIn">Your surname is:</label>
        <input type="text" v-model="computedSurname" placeholder="Insert new surname.." />
        <p>{{surname}} {{surnameChanged}}</p>
      </div>
      <label v-if="$store.state.isLoggedIn">Your username is:</label>
      <input type="text" v-model="computedUsername" placeholder="Insert new username.." />
      <p>{{username}} {{usernameChanged}}</p>
    </div>
    <div>
      <label v-if="$store.state.isLoggedIn">Your password is not visible:</label>
      <input type="password" v-model="computedPassword" placeholder="Insert new password.." />
      <p>{{password}} {{passwordChanged}}</p>
    </div>
    <div>
      <input type="radio" value="1" name="rola" v-model="rolaName"/>Admin 
      <input type="radio" value="2" name="rola" v-model="rolaName"/>User
    </div>
    <input type="button" value="submit" @click="update()" />
  </div>
</template>

<script>
export default {
  data(){
    return{
      rolaName: null
    }
  }
};
</script>

<style>
</style>