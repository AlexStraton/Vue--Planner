<template>
  <div class="project">
    <div @click="handleClick" class="title">
      <h3>{{ project.title }}</h3>
    </div>
    <div v-if="visibility" class="visibility">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      visibility: false,
    };
  },
  methods: {
    handleClick() {
      this.visibility = !this.visibility;
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.visibility {
  visibility: visible;
}
</style>
