<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newPostParams)
        .then((response) => {
          console.log("Success", response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div>
    <h1>New Post</h1>
    <form v-on:submit.prevent="createPosts()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div>
        Title:
        <input type="text" v-model="newPostParams.title" />
        <br />
      </div>
      <div>
        Body:
        <input type="text" v-model="newPostParams.body" />
        <br />
        <small class="test-danger" v-if="newPostParams.body && newPostParams.body.length < 100">
          Must be at least 100 characters
        </small>
        <br />
        <small class="test-danger" v-if="newPostParams.body && newPostParams.body.length > 500">
          Must be no more 500 characters
        </small>
      </div>
      <div>
        Image:
        <input type="text" v-model="newPostParams.image" />
        <br />
      </div>
      <input type="submit" value="Submit Post" />
    </form>
  </div>
</template>
