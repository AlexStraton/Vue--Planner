<template>
  <div class="home">Home</div>
  <div v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
      <SingleProject :project="project" />
    </div>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue";

export default {
  name: "home",
  components: { SingleProject },
  data() {
    return {
      projects: [],
    };
  },
  async mounted() {
    const data = await fetch("http://localhost:3000/projects");
    const parsedData = await data.json();

    this.projects = parsedData;
  },
};
</script>
