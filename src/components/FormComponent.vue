<template>
  <section>
    <div class="container">
      <form @submit.prevent="addTask" class="app__form">
        <input
          type="text"
          required
          v-model="task"
          placeholder="add your new todo"
        />
        <button>+</button>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  name: "FormComponent",
  data() {
    return {
      task: null,
    };
  },
  methods: {
    addTask() {
      this.$emit("sendTask", this.task);
      this.task = null;
    },
  },
};
</script>

<style scoped></style>
