<template>
  <div class="project">
    <div class="title_icons">
      <h3 @click="handleClick">{{ project.title }}</h3>
      <div class="icons">
        <span
          @click="handleEdit"
          class="material-symbols-outlined material-icons"
          >edit</span
        >
        <span
          @click="deleteProject"
          class="material-symbols-outlined material-icons">
          delete
        </span>
        <span
          @click="handleTick"
          class="material-symbols-outlined material-icons tick"
          :class="{ done: ticked }">
          done
        </span>
      </div>
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
      ticked: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    handleClick() {
      this.visibility = !this.visibility;
    },
    async deleteProject() {
      try {
        const data = await fetch(this.url, { method: "DELETE" });
        this.$emit("delete", this.project.id);
      } catch (error) {
        console.log(error);
      }
    },
    handleEdit() {},
    handleTick() {
      this.ticked = !this.ticked;
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
.title_icons {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  font-size: 35px;
  cursor: pointer;
  font-weight: 500;
}
.material-icons:hover {
  color: #e90074;
}
.tick {
  font-weight: 900;
}
.done {
  background-color: rgba(112, 243, 89, 0.7);
}
</style>

<!-- {
  "projects": [
    {
      "id": 1,
      "title": "Create new homepage banner",
      "details": "Lorem ipsum",
      "complete": false
    },
    {
      "id": 2,
      "title": "Make marketing email",
      "details": "Lorem ipsum",
      "complete": true
    }
  ]
} -->
