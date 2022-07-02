<template>
  <div class="single-page">
    <img :src="'/storage/' + post.cover_image" :alt="post.title" />
    <h1>{{ post.title }}</h1>
    <p>{{ post.content }}</p>
    <span>Categories:{{ post.category.name }}</span>
    <div class="tags" v-if="post.tags.length > 0">
      <ul>
        <strong>Tags:</strong>
        <li v-for="tag in post.tags">
        {{tag.name}}
        </li>
      </ul>
    </div>
    <div class="no-tags">
        <strong>tags n/a</strong>
    </div>
  </div>
</template>

<script>
import Axios from "axios";

export default {
  name: "Post",
  data() {
    return {
      post: "",
    };
  },
  mounted() {
    Axios.get("/api/posts/" + this.$route.params.slug)
      .then((response) => {
        console.log(response);
        this.post = response.data;
      })
      .catch((e) => {
        console.error(e);
      });
  },
};
</script>