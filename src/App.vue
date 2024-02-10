<template>
  <section class="todo-container">
    <h1 class="heading">todo app</h1>
    <div class="inner-todo-container">
      <div class="inputContainer">
        <input v-model="taskValue" type="text" placeholder="Enter your task" class="main-input" />
        <button @click="addTask()" class="addBtn">
          <i class="fas fa-plus"></i>
        </button>
      </div>
      <!-- <InputField @add-new-task="addTask" @edit-task="editTask" /> -->
      <Tasks @tasks-updated="updateTasks" :tasks="tasks" @delete-task="deleteTask" @edit-task="editTask" />
      <!-- <div class="tasksContainer">
        <div class="task-wrapper">
          <p class="task">${task}</p>
          <div class="icon-pack">
            <button class="editBtn">
              <i class="fas fa-pen"></i>
            </button>
            <input type="checkbox" class="i-check" />
            <button class="deleteBtn">
              <i class="fas fa-trash"></i>
            </button>
          </div>
        </div>
      </div> -->
      <div class="task-status-wrapper">
        <span class="task-status"> {{ this.tasks.filter((task) => task.checked == true).length }} out of {{
          this.tasks.length }} tasks completed </span>
      </div>
    </div>
  </section>
</template>

<script>

import Tasks from "./components/Tasks.vue"

export default {
  name: 'App',
  components: {
    Tasks
  },
  data() {
    return {
      taskValue: "",
      tasks: [],
      shouldBeEdited: false,
      taskToBeEditedId: null,
      noOfCompletedTasks: 0
    }
  },
  methods: {
    addTask() {
      if (!this.taskValue) {
        return
      }
      else {
        if (this.shouldBeEdited) {
          const listOfTasksCopy = [...this.tasks]
          const actualTaskObj = listOfTasksCopy.find((task) => task.id == this.taskToBeEditedId)
          actualTaskObj.taskValue = this.taskValue
          this.tasks = listOfTasksCopy
          this.shouldBeEdited = false
          this.taskToBeEditedId = null
          // console.log(this.tasks);
        }
        else {
          const newTask = {
            id: Math.random().toFixed(4),
            taskValue: this.taskValue,
            checked: false
          }
          // this.$emit('add-new-task', newTask)
          this.tasks = [...this.tasks, newTask]
          // console.log(newTask);
          // console.log(this.tasks);

        }
        this.taskValue = ""
      }
    },

    // addTask(task) {
    //   this.tasks = [...this.tasks, task]
    //   console.log(this.tasks);
    // },

    deleteTask(id) {
      console.log(id);
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
      })
    },

    editTask(id, value) {
      // this.tasks = this.tasks.map((task) => {
      //   if (task.id == id) {
      //     return { ...task, taskValue: value }
      //   }
      //   return task
      // })
      console.log(id, value);
      this.taskValue = value
      this.shouldBeEdited = true
      this.taskToBeEditedId = id
    },

    updateTasks(updatedTasks) {
      this.tasks = updatedTasks;
      console.log(this.tasks);
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  text-decoration: none;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

body {
  background: #E3E9FF;
  font-family: 'Open Sans', sans-serif
}


.todo-container {
  padding-block: 7rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.todo-container .heading {
  text-transform: uppercase;
  font-size: 3rem;
  color: #757575;
  font-weight: bold;
}

.todo-container .inner-todo-container {
  display: flex;
  position: relative;
  flex-direction: column;
  gap: 2rem;
  width: 400px;
  background: #AF7EEB;
  padding-top: 2rem;
  padding-bottom: 4rem;
  padding-inline: 3rem;
  color: white;
}

.todo-container .inner-todo-container .task-status-wrapper {
  position: absolute;
  text-align: center;
  left: 0;
  bottom: 1rem;
  left: 50%;
  transform: translateX(-50%);
}

.todo-container .inner-todo-container .task-status-wrapper .task-status {
  font-size: 1.3rem;
}


.todo-container .inner-todo-container .inputContainer {
  width: 100%;
  background: white;
  color: black;
  display: flex;
  align-items: center;
  height: 40px;
  padding-inline: 1rem;
}


.todo-container .inner-todo-container .inputContainer .main-input {
  padding: .2rem;
  width: 94%;
  height: 100%;
  border: none;
  outline: none;
}

.todo-container .inner-todo-container .inputContainer .addBtn {
  border: none;
  background: #C8ABFD;
  color: white;
  font-weight: bold;
  padding: .4rem .5rem;
  cursor: pointer;
}
</style>
