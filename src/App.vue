<template>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/> -->
  <!-- <div v-html="message"></div>
  <div>{{ discount }}</div>
  <input v-model="num1" type="text" />
  <input v-model="num2" type="text" />
  <button @click="add">Add Discount</button> -->
  <div>Simple to DO</div>
  <input v-model="todo" type="text" @keyup.enter="add" />
  <button @click="add">Add</button>
  <list :todos="list" @deletetodo="deletetodo" @donetodo="donetodo" />
  <div>Total Todo = {{ totaltodo }}</div>
  <!-- <div>name : {{ name }}</div>
  <div>age : {{ age }}</div>
  <div>Count : {{ nilai }}</div>
  <button @click="add">Add</button>
  <div>result : {{ result }}</div> -->
  <list />
</template>
<script>
import List from "./components/List.vue";
import { ref, reactive, onMounted, computed, toRefs } from "vue";
export default {
  components: {
    List,
  },
  setup() {
    const todo = ref("");
    const todos = reactive({
      list: [],
    });
    onMounted(() => {
      const items = localStorage.getItem("todo");
      todos.list = items ? JSON.parse(items) : [];
    });
    const totaltodo = computed(() => {
      return todos.list.length;
    });

    const add = () => {
      todos.list.unshift({
        acttifity: todo.value,
        isDone: false,
      });
      todo.value = "";
      saveLocal();
    };
    const deletetodo = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      saveLocal();
    };
    const donetodo = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = !item.isDone;
        }
        return item;
      });
      saveLocal();
    };
    const saveLocal = () => {
      localStorage.setItem("todo", JSON.stringify(todos.list));
    };

    return {
      todo,
      ...toRefs(todos),
      totaltodo,
      add,
      donetodo,
      deletetodo,
      donetodo,
    };
  },
};
</script>
<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
