<template>
    <button class="btn" @click="showForm = !showForm">
        {{ showForm ? 'Cancel' : 'Add Task' }}
    </button>
    <div class="form-container">
        <form v-if="showForm" @submit.prevent="addTask">
            <input v-model="newTask.text" type="text" placeholder="Task name" />
            <input v-model="newTask.day" type="text" placeholder="Task day" />
            <button type="submit" class="btn" :style="{ backgroundColor: buttonColor }">Save Task</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'Button',
    props: {
        buttonText: String,
        buttonColor: String,
        tasks: Array, // Receive tasks as a prop
    },
    data() {
        return {
            showForm: false,
            newTask: {
                text: '',
                day: '',
                reminder: false,
            },
        };
    },
    methods: {
        addTask() {
            if (this.newTask.text.trim() === '') {
                return;
            }

            this.$emit('add-task', this.newTask);
            this.newTask = {
                text: '',
                day: '',
                reminder: false,
            };
            this.showForm = false;
        },
    },
}
</script>