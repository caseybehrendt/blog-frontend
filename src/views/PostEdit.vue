<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      errors: [],
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/posts/" + this.$route.params.id + "json").then((response) => {
        this.post = response.data;
        console.log("One Post: ", response.data);
      });
    },
    editPost: function () {
      axios
        .patch("/posts/" + this.post.id + ".json", this.post)
        .then((response) => {
          console.log("Success!", response.data);
          this.$router.push("/recipes");
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
    <h1>Edit Post</h1>
    <form v-on:submit.prevent="editPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div>
        Title:
        <input type="text" v-model="post.title" />
      </div>
      <div>
        Body:
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        Image:
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit Post" />
    </form>
  </div>
</template>

<style scoped></style>
