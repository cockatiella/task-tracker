<template>
    <div :class="['task', { 'completed': task.reminder }]">
        <h3>
            {{ task.text }}
            <i @click="onDelete" class="fa-solid fa-xmark"></i>
            <i @click="onDone" class="fa-solid fa-check"></i>
        </h3>
        <p>{{ task.day }}</p>
    </div>
</template>
  
<script>
export default {
    name: 'Task',
    props: {
        task: Object
    },
    methods: {
        onDelete() {
            this.$emit('delete-task', this.task.id);
        },
        onDone() {
            this.$emit('done-task', this.task.id);
        }
    }
}
</script>
  
<style scoped>
.completed {
    text-decoration: line-through;
    background-color: #ccc;
    /* Adjust the background color as needed */
    /* You can add other styles for completed tasks */
}
</style>
  