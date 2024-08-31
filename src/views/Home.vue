<template>
  <div class="home">Home</div>
  <div v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
      <p>{{ project.title }}</p>
      <p>{{ project.details }}</p>
      <p>{{ project.complete }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "home",
  components: {},
  data() {
    return {
      projects: [],
    };
  },
  async mounted() {
    const data = await fetch("http://localhost:3000/projects");
    const parsedData = await data.json();
    console.log(parsedData);
    this.projects = parsedData;
  },
};
</script>
