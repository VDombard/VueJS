<template>
  <div id="destlist"> <h1>Liste des destinations</h1>
  <div v-for="(dest, iddest) in destlist" :key="dest.idcountry">
          {{ dest.country }}
  </div>
  </div>
</template>

<script>
    import axios from "axios";
    //import dest from "./Dest";

    export default {
        name: "Destlist",
        //components: { Dest },
        data() {
            return {
                destlist: [],
                url:"http://localhost:8000/api/homepage"
            }
        },
        methods: {
            get_destlist() {
                axios
                .get(this.url)
                .then ( (response) => {
                    this.destlist = response.data;
                    console.log(this.destlist);
                })
                .catch( (error) => {
                    console.log(error);
                })
            }
        },
        mounted() {
            this.get_destlist();
        }
}
</script>

<style>
#destlist {
    background-color: lightblue;
    margin: 10px auto;
    padding: 10px;
    width: 500px;
}
</style>