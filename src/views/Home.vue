<template>
  <div class="home">Home</div>
  <FilterNav @filterChange="current = $event" :current="current" />
  <div v-if="projects.length">
    <div v-for="project in filteredProjects" :key="project.id">
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
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: "home",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
      filteredProjects: [],
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
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.complete);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.complete);
      }
      return this.projects;
    },
  },
};
</script>
<style scoped>
.home {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  font-size: 3rem;
  color: rgb(105, 107, 112);
  font-weight: 800;
  text-align: center;
}
</style>
