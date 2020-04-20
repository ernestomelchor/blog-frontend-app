<template>
  <div class="posts-show">
    <h1>Blog Post</h1>
    <h2>{{ post.title }}</h2>
    <p>{{ post.body }}</p>
    <img v-bind:src="post.image" alt />
    <div>
      <a href="/posts">Return to All Posts</a>
    </div>
    <div>
      <a v-bind:href="`/posts/${post.id}/edit`">Edit This Post</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {}
    };
  },
  created: function() {
    this.showPost();
  },
  methods: {
    showPost: function() {
      axios.get("/api/posts/" + this.$route.params.id).then(response => {
        console.log("Get one post!", response);
        this.post = response.data;
      });
    }
  }
};
</script>
