<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link v-if="$store.state.isLoggedIn" to="/update">Profile</router-link>
        <span v-if="$store.state.isLoggedIn"> | </span>
      <router-link v-if="$store.state.isAdmin" to="/admin">Admin Page</router-link> 
        <span v-if="$store.state.isAdmin"> | </span>     
      <router-link to="/login" v-if="!$store.state.isLoggedIn">Login</router-link> 
      <router-link to="/login" v-else>Logout</router-link> |
      <router-link to="/registartion">Registration</router-link> <!-- nemam mounted nego created-->
    </div>
      <router-view/>
  </div>
</template>

<style>
*{
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-image: url("./assets/sea.jpg");
  background-repeat: no-repeat;
  background-position: center;
  height: 100vh;
  width: 100%;

}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  /* color: #42b983; */
  color: #ccccff
}
</style>
