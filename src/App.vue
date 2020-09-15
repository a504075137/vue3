<template>
  <h1>todolist</h1>
  <input type="text" v-model="newTodo" @keyup.enter="addTodo" />
  <ul>
    <li
      :class="{done:item.complete}"
      @click="toggle(index)"
      v-for="(item,index) in todos"
      :key="item.id"
    >{{item.title}}</li>
  </ul>
  <div>{{remaining}}</div>
</template>

<script>
import { ref, reactive, toRefs, computed } from "vue";
import addTodoFac from "./addTodo";
export default {
  name: "App",
  components: {},
  setup() {
    const state = reactive({
      newTodo: "",
      todos: [
        {
          id: 1,
          title: "吃饭",
          complete: true,
        },
        {
          id: 2,
          title: "喝水",
          complete: false,
        },
        {
          id: 3,
          title: "睡觉",
          complete: false,
        },
      ],
    });

    const { addTodo } = addTodoFac(state);
    function toggle(i) {
      state.todos[i].complete = !state.todos[i].complete;
    }

    const remaining = computed(
      () => state.todos.filter((todo) => !todo.complete).length
    );
    // return { state, addTodo };
    return { ...toRefs(state), addTodo, remaining, toggle };
  },
};
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>
