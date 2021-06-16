<template>
  <div class="signup">
    <img v-if="status" v-bind:src="`https://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="submit()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="string" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body</label>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <label>Image url:</label>
        <input type="text" v-model="newPostParams.image_url" />
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
      name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      console.log("These are my Params", this.NewPostParams);
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post("/users", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
