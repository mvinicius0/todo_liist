<script>
import TodoEmpty from "./components/TodoEmpty.vue";
import TodoFormAdd from "./components/TodoFormAdd.vue";
import TodoItems from "./components/TodoItems.vue";
import TodoSpinner from "./components/TodoSpinner.vue";
import axios from "axios";

export default {
  components: {
    TodoFormAdd,
    TodoItems,
    TodoSpinner,
    TodoEmpty,
  },

  data() {
    return {
      loading: false,
    };
  },

  created() {
    this.loading = true;
    this.$store.dispatch("getTodos").finally(() => {
      this.loading = false;
    });
  },
};
</script>

<template>
  <div class="px-3 py-10 md:px-10">
    <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
      <TodoSpinner v-if="loading" />
      <template v-else>
        <TodoFormAdd />

        <TodoItems />

        <TodoEmpty />
      </template>
    </div>
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
