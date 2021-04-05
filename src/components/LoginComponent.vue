<template>
  <div class="login">
    <h1>Login Component!</h1>
    <form>
      <div class="form-group">
        <label for="exampleInputEmail1">Email address</label>
        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter User" required>
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
      </div>
      <button type="submit" class="btn btn-outline-primary" v-on:click="login">
        <router-link to="/logged">Login</router-link>
      </button>
      <div>
        <router-link to="/">Go to Bar</router-link>
      </div>
    </form>
    <!-- route outlet -->
    <!-- component matched by the route will render here -->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'LoginComponent',
  data() {
    return {
      userName: '',
      password: ''
    }
  },
  methods: {
    login() {
      this.userName = document.getElementById('username').value;
      this.password = document.getElementById('pass').value;
      sessionStorage.setItem('currentUserLogged', this.userName);
      if (this.userName in sessionStorage) {
        alert('User already exist!');
      }
      console.log(`${this.userName} & ${this.password}`);
    }
  }
}

</script>