<template>
  <div id="destlist"> <h1>Liste des destinations</h1>

        <button v-on:click="showCreate = ! showCreate">Create destination</button>
        <div v-if="showCreate">
            <input type="number" v-model="dest.fkuser">
            <input type="number" v-model="dest.fkagence">
            <input type="text" v-model="dest.country">
            <input type="text" v-model="dest.city">
            <input type="text" v-model="dest.days">
            <button v-on:click="destAdd">Sauver</button>
        </div>

        <div v-for="dest in destlist">
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
                    iddestination: 0,
                    fkuser: "",
                    fkagence: "",
                    country:"country",
                    city: "city",
                    days: "days"

                },
                destlist: [],
                url:"http://localhost:8000/api/homepage/",
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
                console.log(dest)
                axios.put(this.url + dest.iddestination, dest)
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
                    console.log(response.data);
                    this.get_destlist();
                })
                .catch( (error) => {
                    console.log(error);
                })
            },
            destDelete(iddestination) {
                axios.delete(this.url + iddestination)
                .then ( (response) => {
                    console.log(response.data);
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