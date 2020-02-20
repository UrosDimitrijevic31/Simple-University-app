<template>
  <div class="home">
    <HelloWorld msg="Welcome to site for TRAVELING"/>
    
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  // mounted(){
  // this.users();
  // },
  
}
</script>

<style scoped>

</style>
