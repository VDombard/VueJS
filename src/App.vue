<template>
  <div id="app"><h1>Gestion des destinations</h1>
  <Destlist></Destlist> <Agencelist></Agencelist>
  </div>
</template>

<script>
import Destlist from "./Destlist";
import Agencelist from "./Agencelist";

export default {
  name: "app",
  components: {Destlist, Agencelist},
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background-color: skyblue;
  margin: 10px auto;
  padding: 10px;
}

</style>
