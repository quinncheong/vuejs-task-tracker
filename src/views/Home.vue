<template>
    <AddTask 
        v-show="showAddTask"
        @add-task='addTask' 
    />
    <Tasks 
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask" 
      :tasks="tasks" 
    />
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'

export default {
    name: 'Home',
    props: {
        showAddTask: Boolean
    },
    components: {
        Tasks,
        AddTask
    },
    data() {
        return {
            tasks: [],
        }
    },
    methods: {
        addTask(task) {
        this.tasks = [...this.tasks, task]
        },
        deleteTask(id) {
        if (confirm('Are you sure?')) {
            this.tasks = this.tasks.filter((task) => task.id !== id )
        }
        },
        toggleReminder(id) {
        this.tasks = this.tasks.map(task => {
            return task.id === id ? { ...task, reminder: !task.reminder } : task
        })

        console.log(id)
        }
    },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appt',
        day: 'March 1st 230pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'School Meeting',
        day: 'March 3rd 130pm',
        reminder: true,
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'March 3rd 11am',
        reminder: false,
      },
    ] 
  }
}
</script>