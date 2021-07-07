<template>
  <div>
    <h1>Minha lista de tarefas</h1>
    <button @click="handleShowHideList">Ver a lista!</button>
    <br />
    <input
      type="text"
      @keyup.enter="addTask"
      v-focus
      v-model="state.currentTask"
    />
    <ul v-if="state.showList">
      <li
        v-for="(task, index) in state.tasks"
        :key="`${task}-${index}`"
        @dblclick="complete(task)"
        class="task-item"
        :class="{ 'line-through': task.isDone }"
      >
        {{ task.name }}
        <button @click="remove(task)">&times;</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { reactive } from "@vue/reactivity";
const focus = {
  inserted: (el) => {
    el.focus();
  },
};

export default {
  directives: {
    focus,
  },
  setup() {
    const state = reactive({
      tasks: [
        { name: "Fazer o curso", isDone: false },
        { name: "Fazer o curso 2", isDone: false },
      ],
      showList: false,
      currentTask: "",
    });

    function handleShowHideList() {
      state.showList = !state.showList;
    }
    function addTask() {
      state.tasks.push({ name: state.currentTask, isDone: false });
      state.currentTask = "";
    }
    function complete(task) {
      state.tasks = state.tasks.map((t) => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone };
        }
        return { ...t };
      });
    }
    function remove(task) {
      state.tasks = state.tasks.filter((t) => t.name !== task.name);
    }

    return { state, handleShowHideList, addTask, complete, remove };
  },
};
</script>

<style scoped>
.task-item {
  cursor: pointer;
  user-select: none;
}

.line-through {
  text-decoration: line-through;
}
</style>
