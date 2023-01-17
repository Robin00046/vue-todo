<template>
  <div>
    <ul v-for="(todo, index) in todos" :key="index">
      <li>
        <span v-if="todo.isDone">
          <b> {{ todo.acttifity }} </b></span
        >

        <span v-else> {{ todo.acttifity }} </span>
        <button style="background-color: #4caf50" @click="donetodo(index)">
          Done
        </button>
        <button style="background-color: red" @click="deletetodo(index)">
          Aku
        </button>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },
  setup(props, { emit }) {
    const deletetodo = (index) => {
      emit("deletetodo", index);
    };
    const donetodo = (index) => {
      emit("donetodo", index);
    };

    return {
      donetodo,
      deletetodo,
    };
  },
};
</script>
