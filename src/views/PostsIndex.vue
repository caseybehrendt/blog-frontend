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
      axios.get("/posts.json").then((response) => {
        this.posts = response.data;
        console.log("All Posts: ", response.data);
      });
    },
  },
};
</script>

<template>
  <div>
    <div class="row">
      <!-- <div class="col-sm-4" v-for="post in posts" v-bind:key="post.id">
        <div class="card md-4"> -->
      <div class="col-sm-4" v-for="post in posts" v-bind:key="post.id" v-on:mouseover="currentPost = Post">
        <div class="card md-4" v-bind:class="{ selected: post == currentPost }">
          <img class="card-img-top" v-bind:src="post.image" v-bind:alt="post.title" />
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{ post.body }}</p>
            <a v-bind:href="`/posts/${post.id}`">More info</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card im {
  object-fit: cover;
  height: 250px;
}
.selected {
  background-color: deepskyblue;
  transition: background-color 1s ease;
}
</style>
