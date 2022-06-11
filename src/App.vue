<template>
  <main class="app">
    <div class="container">
      <h1>{{ title }}</h1>
      <p class="msg">{{ msg }} <span v-show="writer">|</span></p>
    </div>
    <FormComponent @sendTask="addTask" />
    <TasksList :tasks="tasks" @deleteTask="deleteTask" />
    <section class="app__result" v-if="tasks.length != 0">
      <div class="container">
        <p>You have {{ tasks.length }} bending tasks</p>
        <button @click="clearTasks">clear</button>
      </div>
    </section>
  </main>
</template>

<script>
import FormComponent from "./components/FormComponent.vue";
import TasksList from "./components/TasksList.vue";

export default {
  name: "App",
  components: {
    FormComponent,
    TasksList,
  },
  data() {
    return {
      title: "TO DO APP",
      message: "Devoloped by ahmed eltaieb",
      msg: "",
      tasks: [],
      writer: false,
    };
  },
  methods: {
    addTask(value) {
      this.tasks.push(value);
      localStorage.tasks = JSON.stringify(this.tasks);
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      localStorage.tasks = JSON.stringify(this.tasks);
    },
    clearTasks() {
      this.tasks = [];
      localStorage.tasks = JSON.stringify(this.tasks);
    },
  },
  beforeMount() {
    if (localStorage.getItem("tasks")) {
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    } else {
      this.tasks = ["hello world", "ahmed eltaieb", "Learn Vue js"];
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    }
  },
  mounted() {
    setInterval(() => {
      this.writer = !this.writer;
    }, 300);
    for (let i = 0; i < this.message.length; i++) {
      setTimeout(() => {
        this.msg += this.message[i];
      }, i * 300);
    }
  },
};
</script>

<style lang="postcss">
:root {
  --main-color: #6600eb;
  --secondary-color: #00bcd4;
}
* {
  margin: 0;
  padding: 0;
  list-style: none;
}
body {
  background: linear-gradient(to bottom, #68eacc 0%, #1b3263 100%);
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.app {
  background-color: #fff;
  min-height: 80px;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  max-height: calc(100vh - 100px);
  & h1 {
    color: var(--main-color);
    margin-bottom: 2px;
  }
  & .msg {
    color: var(--secondary-color);
    margin-bottom: 7px;
    margin-left: 20px;
  }
  & .msg span {
    color: var(--main-color);
  }
  &__form {
    margin: 20px 0;
    display: flex;
    gap: 7px;
    width: 100%;
  }
  &__form input {
    height: 100%;
    outline: none;
    border-radius: 3px;
    border: 1px solid #ccc;
    font-size: 21px;
    text-align: center;
    transition: all 0.3s ease;
  }
  &__form input:focus {
    border-color: var(--main-color);
  }
  &__form button {
    width: 50px;
    height: 100%;
    border: none;
    color: #fff;
    font-size: 21px;
    outline: none;
    background: var(--main-color);
    cursor: pointer;
    border-radius: 3px;
    transition: all 0.3s ease;
  }
  &__form button:hover {
    background: var(--secondary-color);
  }
  &__tasks-list ul {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    max-height: 50vh;
    overflow-y: auto;
  }
  &__tasks-list li {
    width: 90%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    word-break: break-all;
    margin: 10px 0;
    padding: 10px;
    border-radius: 3px;
    background: #fff;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  }
  &__tasks-list li:hover {
    background: #f5f5f5;
  }
  &__tasks-list li button {
    border: none;
    outline: none;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  &__result .container {
    display: flex;
    align-items: center;
    margin: 7px 0;
    justify-content: space-between;
  }
  &__result p {
    font-size: 21px;
    color: var(--main-color);
  }
  &__result button {
    border: none;
    outline: none;
    background: var(--main-color);
    color: #fff;
    font-size: 21px;
    cursor: pointer;
    border-radius: 7px;
    transition: all 0.3s ease;
    padding: 7px;
  }
  &__result button:hover {
    background: var(--secondary-color);
  }
}
@media screen and (max-width: 387px) {
  .app {
    width: calc(100% - 40px);
    margin: auto;
    padding: 20px 10px;
  }
  .app__form {
    flex-direction: column;
    align-items: center;
  }
}
</style>
