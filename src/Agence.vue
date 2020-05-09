<template>
    <div id="agence"><h3>Nom agence: {{ agence.nomagence }} </h3>
    <button v-on:click="showInput = true" v-if="! showInput">Modifier</button>
   
        <div v-if="showInput">
            <input type="text" v-model="agence.nomagence">
            <button v-on:click="updateAgence(agence)">Sauver</button>
        </div>

    </div>
</template>

<script>
    export default {
        name: "Agence",
        props:['agence'],
        data() {
            return {
                showInput:false
            }
        },
        methods: {
            updateAgence(agence) {
                this.$emit('event_update', agence);
                this.showInput = false;
            }
        }
    }
</script>

<style>
#agence {
    background-color: lightgreen;
    margin: 5px auto;
    padding: 5px;
    width: 300px;
}
</style>