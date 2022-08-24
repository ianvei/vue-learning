<script>
import ButtonVue from './ButtonVue.vue'

export default {
    name: 'HeaderComponent',
    props: {
        title: String,
        showAddTask: Boolean,
    },
    components: {
        ButtonVue,
    }
}

</script>

<template>
    <header>
        <h1>{{title}}</h1>
        <ButtonVue @btn-click="$emit('toggle-add-task')" :text="showAddTask? 'Close' : 'Add Task'" :color="showAddTask? 'Red': 'Green'" />
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
