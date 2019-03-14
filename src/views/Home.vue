<template>
    <div>

      <div class="text-center">
        <h1>NestJS Blog</h1>
       <p>A blog website built with Nest.js | Vue.js | MongoDB</p>

       <div v-if="posts.length === 0">
            <h2>No posts found.</h2>
        </div>
      </div>

        <div class="container">
          <div class="row">
            <div class="col-md-4" v-for="post in posts" :key="post._id">
                <div class="card mb-4 shadow-sm">
                  <div class="card-body">
                    <h2 class="card-img-top">{{ post.title }}</h2>
                    <p class="card-text">{{ post.body }}</p>
                    <div class="btn-group">
                      <router-link :to="{name: 'Post', params: {id: post._id}}" class="btn btn-sm btn-outline-secondary">View Post </router-link>
                      <router-link :to="{name: 'Edit', params: {id: post._id}}" class="btn btn-sm btn-outline-secondary">Edit Post </router-link>
                      <button class="btn btn-sm btn-outline-secondary" v-on:click="deletePost(post._id)">Delete Post</button>
                    </div>

                    <div class="card-footer">
                      <small class="text-muted">Posted on: {{ post.date_posted }}</small><br/>
                      <small class="text-muted">by: {{ post.author }}</small>
                    </div>

                  </div>
                </div>
              </div>
          </div>
        </div>
    </div>
</template>

<style>
.btn-group {
  margin-bottom: 20px;
}
</style>

<script>
// @ is an alias to /src
import { server } from "@/utils/helper";
import axios from "axios";

export default {
  data() {
    return {
      posts: []
    };
  },
  created() {
    this.fetchPosts();
  },
  methods: {
    fetchPosts() {
      axios
        .get(`${server.baseURL}/blog/posts`)
        .then(data => (this.posts = data.data));
    },
    deletePost(id) {
      axios.delete(`${server.baseURL}/blog/delete?postID=${id}`).then(data => {
        console.log(data);
        window.location.reload();
      });
    }
  }
};
</script>
