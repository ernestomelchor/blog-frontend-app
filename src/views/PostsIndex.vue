<template>
  <div class="posts-index">
    <h1>All Posts</h1>
    <div v-for="post in posts">
      Title:
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <img v-bind:src="post.image" alt />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      posts: []
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      console.log("Success!", response.data);
      this.posts = response.data;
    });
  },
  methods: {}
};
</script>