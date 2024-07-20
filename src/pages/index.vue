<template>
  <div class="index-page">
    <TheHeader />
    <component
      class="index-page__component"
      :is="component"
      :tasks="tasks"
      @toggle-component="toggleComponent"
      @create-task="onCreateNewTask"
      @delete-task="deleteTask"
      @change-task="changeTask"
    ></component>
  </div>
</template>

<script setup>
import { computed, ref, onMounted } from '/vue';
import ToDo from 'src/widgets/ToDo/Todo.vue';
import AddNewTask from 'src/widgets/ToDo/AddNewTask.vue';
import TheHeader from "../layout/TheHeader.vue";

const componentKey = ref("ToDo");
const component = computed(() =>
  componentKey.value === "ToDo" ? ToDo : AddNewTask,
);
const tasks = ref([]);

function toggleComponent() {
  componentKey.value = componentKey.value === "ToDo" ? "AddNewTask" : "ToDo";
}

function createNewTask(taskName) {
  const task = {
    id: Date.now(),
    name: taskName,
  };
  tasks.value.push(task);
}

function onCreateNewTask(taskName) {
  toggleComponent();
  createNewTask(taskName);
  updateStorageTasks();
}

function deleteTask(index) {
  tasks.value.splice(index, 1);
  updateStorageTasks();
}

function changeTask({ taskIndex, taskName }) {
  const task = tasks.value[taskIndex];
  if (task) {
    task.name = taskName;
    updateStorageTasks();
  }
}

function getTasksFromStorage() {
  const tasksFromStorage = localStorage.getItem("tasks") ?? [];
  tasks.value = JSON.parse(tasksFromStorage);
}

function updateStorageTasks() {
  const newTasks = JSON.stringify(tasks.value);
  localStorage.setItem("tasks", newTasks);
}

onMounted(() => {
  getTasksFromStorage();
});
</script>

<style scoped>
.index-page {
  min-height: 100dvh;
  display: flex;
  flex-direction: column;
}

.index-page__component {
  flex-grow: 1;
  padding: 20px;
}
</style>
