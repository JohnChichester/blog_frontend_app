<template>
  <div>
    <h1>One post</h1>
    <h2>{{ post.title }}</h2>
    <div>
      <img v-bind:src="post.image_url" alt="post.title" />
    </div>
    <a href="/posts">Back to Blog</a>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      postss: [],
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPosts: function () {
      axios.get("/posts/1").then((response) => {
        console.log("show posts", response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
