<script>
import ButtonVue from './ButtonVue.vue'

export default {
    name: 'HeaderComponent',
    props: {
        title: String,
    },
    components: {
        ButtonVue,
    }
}

</script>

<template>
    <header>
        <h1>{{title}}</h1>
        <ButtonVue @toggle-add-task="$emit('toggle-add-task')" text="Add Task" color="Green" />
    </header>
</template>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>
