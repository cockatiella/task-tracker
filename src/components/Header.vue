<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @add-task="addTask" :buttonText="'Add Task'" :buttonColor="'rgb(173, 173, 240)'" :tasks="tasks" />
    </header>
</template>

<script>
import Button from './Button.vue';


export default {
    name: 'Header',
    props: {
        title: String,
        tasks: Array
    },
    components: {
        Button,
    },
    emits: ['add-task'], // Declare 'add-task' as an emitted event
    methods: {
        addTask(newTask) {
            // Generate a unique ID for the new task
            const id = Math.max(...this.tasks.map((task) => task.id), 0) + 1;
            newTask.id = id;
            this.tasks.push(newTask);
        },
    },
}
</script>

<style scoped>
header {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    width: 100%;
    align-items: center;
    margin-bottom: 1rem;
}
</style>