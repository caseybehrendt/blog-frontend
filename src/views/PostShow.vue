<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
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
    destroyPost: function () {
      axios.delete("/posts/" + this.$route.params.id + "json").then((response) => {
        console.log(response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>

<template>
  <div>
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image_url" v-bind:alt="post.title" />
    <p>Body: {{ post.body }}</p>
    <a v-bind:href="`/posts/${post.id}/edit`">Edit Post</a>
    <button v-on:click="destroyPost()">Delete Post</button>
    <a href="/posts">Back to All Posts</a>
  </div>
</template>

<style scoped></style>
