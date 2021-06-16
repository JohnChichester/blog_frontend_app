<template>
  <div class="home">
    <!-- <img v-if="status" v-bind:src="`https://http.cat/${status}`" alt="" /> -->
    <!-- <div>
      <h1>New Post</h1>
      Title
      <input type="text" v-model="newPostTitle" />
      Body
      <input type="text" v-model="newPostBody" />
      Image
      <input type="string" v-model="newPostImage" />
      <button v-on:click="createPost()">Create</button>
    </div> -->

    <h1>All posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <img class="post-image" v-bind:src="post.image_url" v-bind:alt="post.title" />
      <div>
        <button v-on:click="showPost(post)">More info</button>
      </div>
    </div>

    <dialog id="post-details">
      <form method="dialog">
        <h1>Post info</h1>
        <p>
          Title:
          <input type="text" v-model="currentPost.title" />
        </p>
        <p>
          Image:
          <input type="text" v-model="currentPost.image_url" />
        </p>
        <p>
          Body:
          <input type="text" v-model="currentPost.body" />
        </p>
        <button v-on:click="updatePost(currentPost)">Update</button>
        <button v-on:click="destroyPost(currentPost)">Destroy</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
.post-image {
  width: 200px;
}
,
.post-details {
  transition: opacity 200ms;
}
</style>
w
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      currentPost: {},
      newPostTitle: "",
      newPostBody: "",
      newPostImageURL: "",
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts", this.posts);
      });
    },
    showPost: function (post) {
      console.log("hello", post);
      this.currentPost = post;
      document.querySelector("#post-details").showModal();
    },
  },
};
</script>
