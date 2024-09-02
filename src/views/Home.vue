<template>
  <div class="home">Home</div>
  <div v-if="projects.length">
    <div v-for="project in projects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="handleDelete"
        @patch="handlePatch"
        @post="handlePost" />
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
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
      console.log(this.projects);
    },
    handlePatch(updatedProject) {
      this.projects = this.projects.map((project) => {
        if (project.id === updatedProject.id) {
          return { ...project, complete: updatedProject.complete };
        } else {
          return project;
        }
      });
    },
    handlePost(newProject) {
      projects.push(newProject);
    },
  },
};
</script>
<style scoped>
.home {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  font-size: 3rem;
  color: rgb(28, 73, 197);
  font-weight: 800;
  text-align: center;
}
</style>
