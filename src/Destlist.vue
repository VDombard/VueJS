<template>
  <div id="destlist"> <h1>Liste des destinations</h1>

        <button v-on:click="showCreate = ! showCreate">Create destination</button>
        <div v-if="showCreate">
            <input type="text" v-model="dest.country">
            <button v-on:click="destAdd">Sauver</button>
        </div>

        <div v-for="(dest, iddest) in destlist" :key="dest.idcountry">
                <Dest v-bind:dest="dest" @event_update="destUpdate" @event_delete="destDelete"></Dest>
        </div>

  </div>
</template>

<script>
    import axios from "axios";
    import Dest from "./Dest";

    export default {
        name: "Destlist",
        components: { Dest },
        data() {
            return {
                dest: {
                    id: 0,
                    country:"none",
                },
                destlist: [],
                url:"http://localhost:8000/api/homepage",
                showCreate: false
            }
        },
        methods: {
            get_destlist() {
                axios
                .get(this.url)
                .then ( (response) => {
                    this.destlist = response.data.destination;
                    console.log(this.destlist);
                })
                .catch( (error) => {
                    console.log(error);
                })
            },
            destUpdate(dest) {
                axios.put(this.url + dest.idcountry, dest)
                .then( (reponse) => {
                    console.log(response.date);
                    })
                .catch( (error) => {
                    console.log(error);
                })  
            },
            destAdd() {
                axios.post(this.url, this.dest)
                .then ( (response) => {
                    console.log(response.data.destination);
                    this.get_destlist();
                })
                .catch( (error) => {
                    console.log(error);
                })
            },
            destDelete(id) {
                axios.delete(this.url + id)
                .then ( (response) => {
                    console.log(response.data.destination);
                    this.get_destlist();
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