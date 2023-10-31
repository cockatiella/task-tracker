<template>
  <div class="container">
    <Header title="Task Tracker" :tasks="tasks" @add-task="addTask" @delete-task="deleteTask" @done-task="doneTask" />
    <Tasks :tasks="tasks" @delete-task="deleteTask" @done-task="doneTask" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';


export default {
  name: 'App',
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    doneTask(id) {
      const updatedTasks = this.tasks.map((task) => {
        if (task.id === id) {
          task.reminder = !task.reminder;
        }
        return task;
      });
      // Move completed tasks to the bottom of the list
      this.tasks = updatedTasks.sort((a, b) => (a.reminder === b.reminder ? 0 : a.reminder ? 1 : -1));
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        reminder: false,
      },
      {
        id: 2,
        text: 'Interview',
        day: 'March 2nd at 2:30pm',
        reminder: false,
      },
      {
        id: 3,
        text: 'Take your Medication',
        day: 'March 3rd at 2:30pm',
        reminder: false,
      },
      {
        id: 4,
        text: 'Order groceries',
        day: 'March 5th at 4:30pm',
        reminder: false,
      },
    ]
  }
}
</script>