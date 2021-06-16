<template>
  <div>
    <h1>All Posts</h1>
  <div>
    Search by Title:
    <input type ="text" v-model="searchFilter" lists="post-titles" />
    <datalist id ="post-titles">
      <option v-for="post in posts" v-bind:key="post.id">{{ post.title }}</option>
    </datalist>
  </div>
    
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <a v-bind:href="`/posts/${post.id}`">More info</a>
    </div>
  </div>
</template>



<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        console.log("index posts", response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
