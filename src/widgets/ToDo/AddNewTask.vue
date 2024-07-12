<template>
  <div class="add-new-task">
    <button
      @click="$emit('toggle-component')"
      class="add-new-task__return-button"
    >
      <svg
        class="add-new-task__icon"
        width="27"
        height="24"
        viewBox="0 0 27 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M0.939341 10.9393C0.353554 11.5251 0.353554 12.4749 0.939341 13.0607L10.4853 22.6066C11.0711 23.1924 12.0208 23.1924 12.6066 22.6066C13.1924 22.0208 13.1924 21.0711 12.6066 20.4853L4.12132 12L12.6066 3.51472C13.1924 2.92893 13.1924 1.97919 12.6066 1.3934C12.0208 0.807611 11.0711 0.807611 10.4853 1.3934L0.939341 10.9393ZM27 10.5L2 10.5V13.5L27 13.5V10.5Z"
          fill="white"
        />
      </svg>
    </button>
    <div class="add-new-task__container">
      <label for="title" class="add-new-task__label">Введите задачу</label>
      <textarea
        id="title"
        rows="1"
        cols="20"
        name="new-task-name"
        class="add-new-task__name"
        v-model="taskName"
        placeholder="Title"
        required
      >
      </textarea>
      <button @click="onAdd" class="add-new-task__button">ADD</button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";
const taskName = ref("");

const emit = defineEmits(["create-task", "toggle-component"]);

function onAdd() {
  if (taskName.value) {
    emit("create-task", taskName.value);
  }
}
</script>

<style scoped>
.add-new-task {
  background-color: #ffffff;

  @media (min-width: 321px) {
    border: #747bff solid 1px;
    margin: 50px auto;
    padding: 20px;
  }
}

.add-new-task__return-button {
  justify-content: start;
  background-color: #ffffff;
  padding: 0;

  @media (min-width: 700px) {
    margin-left: 25px;
    margin-top: 25px;
  }
}

.add-new-task__return-button path {
  fill: #9395d3;
}

.add-new-task__icon {
  width: 20px;
  height: 20px;

  @media (min-width: 321px) {
    width: 30px;
    height: 30px;
  }
}

.add-new-task__label {
  margin-top: 20px;
  color: #9395d3;
  text-transform: uppercase;
  font-size: 20px;
  font-weight: bold;
}

.add-new-task__name {
  border: none;
  outline: none;
  font-weight: 500;
  font-family: inherit;
  cursor: pointer;
  transition: border 0.2s ease-out;
  flex-grow: 1;
  margin: 40px 30px;
  border-bottom: 2px solid #8b8787;
  padding: 15px;
  resize: none;
  color: #9395d3;
  font-size: 15px;

  @media (min-width: 500px) {
    margin: 40px 40px;
  }
}

.add-new-task__name::-webkit-scrollbar {
  width: 0;
}

.add-new-task__name::placeholder {
  color: #8b8787;
  font-size: 16px;
}

.add-new-task__name:focus,
.add-new-task__name:hover {
  border: 2px solid #747bff;
}

.add-new-task__name:focus::placeholder {
  color: transparent;
}

.add-new-task__button {
  position: relative;
  height: 65px;
  background-color: #9395d3;
  color: white;
  text-align: center;
  border-radius: 15px;
  font-size: 20px;
  width: 100%;
  transition:
    box-shadow 0.2s ease-out,
    top 0.2s ease-out;
}

.add-new-task__button:active {
  box-shadow: rgba(0, 0, 0, 0.15) 2.4px 2.4px 3.2px;
  top: 2px;
}

.add-new-task__button:hover {
  box-shadow: rgba(0, 0, 0, 0.45) 0 25px 20px -20px;
}

.add-new-task__container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: auto;

  @media (min-width: 1000px) {
    padding: 40px;
  }
}
</style>
