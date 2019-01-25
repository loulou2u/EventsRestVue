<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul v-if="posts && posts.length">
      <li v-for="(post, index) in posts" :key="index">
        <p>{{ post.title }}</p>
      </li>
    </ul>

    <ul v-if="errors && errors.length">
      <li v-for="(error, index) in errors" :key="index">{{ error.message }}</li>
    </ul>

    <a href="https://events.rice.edu">More events</a>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Upcoming Events",
      posts: [],
      errors: []
    };
  },
  created() {
    axios
      .get(
        `https://rice.lwcal.com/live/json/events/group/academic calendar/max/4`
      )
      .then(response => {
        // JSON responses are automatically parsed.
        this.posts = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #1a73e8;
}
</style>
