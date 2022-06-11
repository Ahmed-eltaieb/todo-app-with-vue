<template>
  <section class="app__tasks-list">
    <div class="container">
      <ul>
        <li v-for="(task, i) in tasks" :key="i">
          {{ task }}
          <button @click="deleteTask(i)">
            <img src="../assets/x.png" alt="deleteicon" />
          </button>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  name: "TasksList",
  props: {
    tasks: Array,
  },
  methods: {
    deleteTask(index) {
      this.$emit("deleteTask", index);
    },
  },
};
</script>

<style scoped></style>
