<template>
  <div class="hello">
    <h1>My First Component!</h1>
    <div>
      <input type="text" placeholder="Todo" id="todo">
    </div>
    <div>
      <select id="completed">
        <option>true</option>
        <option>false</option>
      </select>
    </div>
    <button @click="addTodo">Add new Todo!</button>
    <button v-on:click="clickBtn">Click Me!</button>
    <ul>
      <li v-for="(todo, index) of todos" :key="todo.id">{{todo.title}}
        <button v-on:click="editTodo(index)">Edit</button>
        <button @click="deleteTodo(index)">Delete</button>
      </li>
    </ul>

    <div v-if="showModal" class="w3-modal">
      <div class="w3-modal-content">
        <div class="w3-container">
          <input type="text" v-model="dataModal">
          <button @click="saveData">Close!</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    userItem: {
      type: Number,
      default: 1,
      dataModal: ''
    },
  },
  data() {
    return {
      todos: [],
      userID: null,
      showModal: false,
      row: null,
      newTodo: '',
      newCompleted: null
    };
  },
  methods: {
    editTodo(row) {
      this.showModal = true;
      this.dataModal = this.todos[row].title;
      localStorage.setItem('user', JSON.stringify(this.row = row));
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem('user', JSON.stringify(this.todos));
    },
    addTodo() {
      this.userID = this.todos.length;
      this.userID++;
      this.newTodo = document.getElementById('todo').value;
      this.newCompleted = document.getElementById('completed').value;
      const newTodo = {
        userId: 1,
        id: this.userID,
        title: this.newTodo,
        completed: this.newCompleted
      }
      this.todos.push(newTodo);
      localStorage.setItem('user', JSON.stringify(this.todos));
    },
    saveData() {
      this.todos[this.row].title = this.dataModal;
      this.showModal = false;
    },
    async clickBtn() {
      try {
        const res = await axios.get(`https://jsonplaceholder.typicode.com/todos?userId=${this.userItem}`);
        window.localStorage.setItem("user", JSON.stringify(res.data));
        console.log(JSON.parse(window.localStorage.getItem("user")));
        this.todos = res.data;
      } catch (e) {
        console.log(`There was an error: ${e}`);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.w3-modal {
  z-index: 3;
  padding-top: 100px;
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0,0,0);
  background-color: rgba(0,0,0,0.4);
}
.w3-modal-content {
  margin: auto;
  background-color: #fff;
  position: relative;
  padding: 0;
  outline: 0;
  width: 600px;
}
</style>
