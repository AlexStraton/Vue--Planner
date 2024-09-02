<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input v-model="title" type="text" />

    <label>details</label>
    <textarea v-model="details">
Details: 
    </textarea>
    <button>Update project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      uri: "http://localhost:3000/projects/" + this.id,
    };
  },
  async mounted() {
    const allProjects = await fetch(this.uri);
    const response = await allProjects.json();

    this.title = response.title;
    this.details = response.details;
  },
  methods: {
    async handleSubmit() {
      console.log("before try");
      try {
        console.log("inside try");
        const response = await fetch(this.uri, {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ title: this.title, details: this.details }),
        });
        console.log(response, "resposne");
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const res = await response.json();
        console.log(res);

        this.$router.push("/");
      } catch (error) {
        console.log(error);
      }
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
