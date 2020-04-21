<template>
  <div class="posts-index">
    <h1>All Posts</h1>
    search:
    <input type="text" v-model="filterText" list="titles" />
    <datalist id="titles">
      <option v-for="post in posts"> {{ post.title }}</option>
    </datalist>
    <div v-for="post in orderBy(filterBy(posts, filterText, 'title'), 'title')">
      <h2>{{ post.title }}</h2>
      <p>Created {{ relativeDate(post.created_at) }}</p>
      <img v-bind:src="post.image" alt />
      <div>
        <a v-bind:href="`/posts/${post.id}`">More info</a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      posts: [],
      filterText: "",
    };
  },
  created: function() {
    axios.get("/api/posts").then((response) => {
      console.log("Success!", response.data);
      this.posts = response.data;
    });
  },
  methods: {
    relativeDate: function(date) {
      return moment(date).fromNow();
    },
  },
};
</script>
