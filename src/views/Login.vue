<template>
  <div class="login">
    <form v-on:submit.prevent="submit()">
      <h1>Login</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Email:</label>
        <input type="email" v-model="email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="password" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        email: "",
        password: "",
        errors: [],
      };
    },
    methods: {
      submit: function () {
        var params = {
          email: this.email,
          password: this.password,
        };
        axios
          .post("/sessions", params)
          .then((response) => {
            axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
            localStorage.setItem("jwt", response.data.jwt);
            this.$router.push("/");
          })
          .catch((error) => {
            console.log(error.response);
            this.errors = ["Invalid email or password."];
            this.email = "";
            this.password = "";
          });
      },
    },
  };
</script>
In src/router/index.js, import the Login.vue component and add a route:

  import Vue from "vue";
  import VueRouter from "vue-router";
  import Home from "../views/home.vue";
  import About from "../views/about.vue";
  import Signup from "../views/signup.vue";
+ import login from "../views/login.vue";

  Vue.use(VueRouter);

  const routes = [
    { path: "/", name: "home", component: Home },
    { path: "/", about", name: "about", component: About },
    { path: "/", signup", name: "signup", component: Signup },
+   { path: "/", login", name: "login", component: login },
  ];