<template>
    <div class="todo-list">
      <h1>Todo List</h1>
      <div>
        <input type="text" class="new-task-input" v-model="newTask" placeholder="Ajouter une tâche">
        <button class="add-task-button" v-on:click="addTask">Ajouter</button>
      </div>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <span v-if="!editing[index]" v-on:dblclick="editTask(index)" v-bind:class="{ 'todo': taskStatus[index] === 'todo', 'in-progress': taskStatus[index] === 'in-progress', 'done': taskStatus[index] === 'done' }">{{ task }}</span>
          <input v-else type="text" v-model="tasks[index]" v-on:keyup.enter="saveTask(index)">
          <div>
              <button v-on:click="setTaskStatus(index, 'todo')" v-bind:class="{ 'active': taskStatus[index] === 'todo' }">À faire</button>
              <button v-on:click="setTaskStatus(index, 'in-progress')" v-bind:class="{ 'active': taskStatus[index] === 'in-progress' }">En cours</button>
              <button v-on:click="setTaskStatus(index, 'done')" v-bind:class="{ 'active': taskStatus[index] === 'done' }">Fait</button>
              <button v-on:click="editTask(index)">Éditer</button>
            <button v-on:click="deleteTask(index)">Supprimer</button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  <script>
  export default {
    data() {
      return {
        tasks: [],
        newTask: '',
        editing: [],
        taskStatus: [],
      };
    },
    methods: {
      addTask() {
        if (this.newTask !== '') {
          this.tasks.push(this.newTask);
          this.taskStatus.push('todo');
          this.newTask = '';
        }
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
        this.editing.splice(index, 1);
        this.taskStatus.splice(index, 1);
      },
      editTask(index) {
        this.$set(this.editing, index, !this.editing[index]);
      },
      saveTask(index) {
        this.editing.splice(index, 1, false);
      },
      setTaskStatus(index, status) {
        this.$set(this.taskStatus, index, status);
      },
    },
  };
</script>
<style>

.todo-list {
  font-family: Arial, sans-serif;
  margin: 50px auto;
  max-width: 600px;
  padding: 20px;
  background-color: rgb(199, 112, 199);
  border-radius: 10px;}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

h2 {
  margin-top: 30px;
}

.new-task-input {
  width: 70%;
  padding: 10px;
  border: none;
  border-radius: 5px;
  margin-right: 10px;

}

.add-task-button {
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  float: right;

}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

span {
  font-size: 18px;
}

input[type="text"] {
    width: 70%;
    padding: 10px;
    border: none;
    border-radius: 5px;
    margin-right: 10px;

  }
  
  button {
    padding: 10px;
    background-color: rgb(67, 185, 196);
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>