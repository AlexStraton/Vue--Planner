<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input v-model="title" type="text" />

    <label>details</label>
    <textarea v-model="details">
Details: 
    </textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  name: "AddProject",
  data() {
    return {
      title: "",
      description: "",
    };
  },
  methods: {
    async handleSubmit() {
      try {
        const response = await fetch("http://localhost:3000/projects", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            title: this.title,
            details: this.details,
            complete: false,
          }),
        });
        const newProject = await response.json();
        console.log(newProject);
        this.$emit("post", newProject);
        this.$router.push("/");
      } catch (error) {
        console.log(error);
      }
      (this.title = ""), (this.details = "");
    },
  },
};
</script>

<style>
form {
  margin-top: 10rem;
  background: white;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}
form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
