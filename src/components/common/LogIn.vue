<template>
  <div id="logIn">
    <div class="col-md-6 card mx-auto">
      <h3 class="card-title">Log In</h3>
      <div class="card-body">
        <div class="form-group">
          <label for="emailInput">Email</label>
          <input v-model='emailInput' type="email" class="form-control" id="emailInput" placeholder="Enter email">
        </div>
        <div class="form-group">
          <label for="passwordInput">Password</label>
          <input v-model='passwordInput' type="password" class="form-control" id="passwordInput" placeholder="Password">
        </div>
      </div>
      <button type="button" class="btn" v-on:click='submit'>Submit</button>
    </div>
  </div>
</template>

<style scoped>
  .card-title {
    margin-top: 10px;
  }

  .btn {
    margin-bottom: 15px;
    width: 100px;
  }
</style>

<script>
  import axios from "axios";
  import { server } from "../../utils/helper";

  export default {
    data: function() {
      return {
        emailInput: "",
        passwordInput: ""
      }
    },

    methods: {
      submit() {
        axios.post(`${server.baseURL}/authenticate`, {
          email: this.emailInput,
          password: this.passwordInput
        })
        .then(
          (res) => console.log("got response:", res),
          (err) => console.log("err:", err)
        );

      },
    }
  }
</script>