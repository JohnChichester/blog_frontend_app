<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">BbLlOoGg</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item active">
            <router-link class="nav-link" to="/posts">All Posts</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/recipes/new">New Post</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
              v-if="!isLoggedIn()"
            >
              Account
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <router-link class="dropdown-item" to="/Login">Login</router-link>
              <router-link class="dropdown-item" to="/Signup">Signup</router-link>
              <!--<div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a> !-->
            </div>
          </li>
          <li class="nav-item" v-if="isLoggedIn()">
            <router-link class="nav-link" to="/logout">Logout</router-link>
          </li>
          <!-- <li class="nav-item">
          <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li> !-->
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>
    <div class="container">
      <!--<div id="nav">
      <router-link to="/Home">Home</router-link>
      |
      <router-link to="/about">About</router-link>
      |
      <router-link to="/Test">Test</router-link>
      |
      <router-link to="/Signup">Signup</router-link>
      |
      <router-link to="/Login">Login</router-link>
    </div>!-->
      <div v-if="flashMessahe" v-on:click="flashMessage = null" class="alert alert-success" role="alert">
        {{ flashMessage }}
      </div>
      <router-view />
    </div>
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      flashMessahe: null,
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
