<template>
    <button  @click="testClick()"  :style="{background: color}">{{text}}</button>
</template>

<script>
    export default {
        name: "ButtonVue",
        props: {
            text: String,
            color: String,
        },
        methods: {
            testClick() {
                this.$emit('btn-click')
                console.log(this.text);
            }
        }
    }

</script>

<style>
   /* button {
    color: props.color;
   } */
</style>