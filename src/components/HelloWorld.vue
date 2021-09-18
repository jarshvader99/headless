<template>
  <div class="hello">
    <div v-for="proj in projects" :key="proj.id">
      <h1>{{ proj.title.rendered }}</h1>
      <img :src="proj.better_featured_image.source_url" />
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      projects: [],
    };
  },
  created: function () {
    this.$http.get("wp/v2/projects").then(
      (response) => {
        for (let project in response.data) {
          this.projects.push(response.data[project]);
        }
      },
      (error) => {
        alert(error);
      }
    );
  },
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
  color: #42b983;
}
</style>
