<template>
    <div id="dest"><h3>{{ dest.country }} </h3>
    </div>
</template>

<script>
    export default {
        name: "Dest",
        props:['dest'],
        data() {
            return {}
        },
        methods: {}
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