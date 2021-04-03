<template>
  <div class="login">
    <div>
      <input type="text" placeholder="User">
    </div>
    <div>
      <input type="password" placeholder="password">
    </div>
    <button v-on:click="login">Login!</button>
  </div>
</template>

<script>

export default {
  name: 'LoginComponent',
  props: {

  },
  data() {
    return {

    }
  },
  methods: {
    login() {
      console.log(`User logged!`);
    }
  }
}

</script>