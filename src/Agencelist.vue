<template>
  <div id="agencelist"> <h1> Liste des agences </h1>

        <button v-on:click="showCreate = ! showCreate">Ajouter une agence</button>
        <div v-if="showCreate">
            <input type="text" v-model="agence.nomagence">
            <button v-on:click="agenceAdd">Sauver</button>
        </div>

        <div v-for="agence in agencelist">
                <Agence v-bind:agence="agence" @event_update="agenceUpdate"></Agence>
        </div>
  </div>
</template>

<script>
    import axios from "axios";
    import Agence from "./Agence";

    export default {
        name: "Agencelist",
        components: { Agence },
        data() {
            return {
                agence: {
                    idagence: 0,
                    nomagence: "nom agence"
                },
                agencelist: [],
                url:"http://localhost:8000/api/agence/",
                showCreate: false
            }
        },
        methods: {
            get_agencelist() {
                axios
                .get(this.url)
                .then ( (response) => {
                    this.agencelist = response.data.agence;
                    console.log(this.agencelist);
                })
                .catch( (error) => {
                    console.log(error);
                })
            },
            agenceUpdate(agence) {
                console.log(agence)
                axios.put(this.url + agence.idagence, agence)
                .then( (reponse) => {
                    console.log(response.data);
                    })
                .catch( (error) => {
                    console.log(error);
                })  
            },
            agenceAdd() {
                axios.post(this.url, this.agence)
                .then ( (response) => {
                    console.log(response.data);
                    this.get_agencelist();
                })
                .catch( (error) => {
                    console.log(error);
                })
            }
        },
        mounted() {
            this.get_agencelist();
        }
}
</script>

<style>
#agencelist {
    background-color: lightseagreen;
    margin: 10px auto;
    padding: 10px;
    width: 500px;
}
</style>