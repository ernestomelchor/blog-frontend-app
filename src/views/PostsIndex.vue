<template>
  <div class="posts-index">
    <h1>All Posts</h1>
    <div v-for="post in posts">
      <h2>{{ post.title }}</h2>
      <img v-bind:src="post.image" alt />
      <div>
        <a v-bind:href="`/posts/${post.id}`">More info</a>
      </div>
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
