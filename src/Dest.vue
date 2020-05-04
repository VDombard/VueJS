<template>
    <div id="dest"><h3>{{ dest.country }} </h3>
    <button v-on:click="showInput = true" v-if="! showInput">Modifier</button>
   
        <div v-if="showInput">
            <input type="text" v-model="dest.country">
            <button v-on:click="updateDest(dest)">Sauver</button>
        </div>
        <button v-on:click="deleteDest(dest.idcountry)">Supprimer</button>

    </div>
</template>

<script>
    export default {
        name: "Dest",
        props:['dest'],
        data() {
            return {
                showInput:false
            }
        },
        methods: {
            updateDest(dest) {
                this.$emit('event_update', dest);
                this.showInput = false;
            },
            deleteDest(iddest) {
                this.$emit('event_delete', iddest);
            }
        }
    }
</script>

<style>
#dest {
    background-color: lightyellow;
    margin: 5px auto;
    padding: 5px;
    width: 300px;
}
</style>