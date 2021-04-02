<template>
  <div class="hello">
    <h1>My First Component!</h1>
    <div>
      <input type="text" placeholder="User">
    </div>
    <div>
      <input type="password" placeholder="Password">
    </div>
    <button>Get Number!</button>
    <button v-on:click="clickBtn">Click Me!</button>
    <ul>
      <li v-for="(todo, index) of todos" :key="todo.id">{{todo.title}}
        <button v-on:click="getId">Edit</button>
        <button @click="deleteTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    userItem: {
      type: Number,
      default: 1
    },
    userID: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    getId() {
      // console.log(this.todos.map((item, index) => {
      //   console.log(`This in the index: ${index} & this is item.id: ${item.id}`);
      // }));
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem('user', JSON.stringify(this.todos));
    },
    async clickBtn() {
      console.log(`Button Clicked! ${this.userItem}`);
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

</style>
