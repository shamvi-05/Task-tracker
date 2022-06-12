<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker"  :showAddTask="showAddTask"   />
      <div v-show="showAddTask">
     <AddTask @add-task ="addTask" />
      </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
   
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask"

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(newTask){
      this.tasks = [...this.tasks, newTask]
    },
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task) => task.id== id ? {...task , reminder: !task.reminder}: task)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctor Appointment ",
        day: "June 10 th at 9:49pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Intern Meet At Zoom ",
        day: "June 10 th at 9:49pm",
        reminder: false,
      },
      {
        id: 3,
        text: "Learn Vue.js For GitLab ",
        day: "June 10 th at 9:49pm",
        reminder: true,
      },
    ];
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
</style>
