<template>
  <div class="todo">
    <transition name="fade" mode="out-in">
      <ul v-if="tasks.length" key="list" class="todo__list">
        <li class="todo__item" v-for="(task, index) in tasks" :key="task.id">
          <Task
            :task-name="task.name"
            @delete-task="$emit('delete-task', index)"
            @change-task="
              $emit('change-task', { taskName: $event, taskIndex: index })
            "
          ></Task>
        </li>
      </ul>
      <p v-else class="todo__text" key="description">
        Нажмите на " + " для добавления задачи
      </p>
    </transition>
    <button class="todo__button-toggle" @click="$emit('toggle-component')">
      <svg
        width="21.000000"
        height="23.625000"
        viewBox="0 0 21 23.625"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
      >
        <defs>
          <filter
            id="filter_2_116_dd"
            x="-0.625000"
            y="3.921875"
            width="22.250000"
            height="23.781250"
            filterUnits="userSpaceOnUse"
            color-interpolation-filters="sRGB"
          >
            <feFlood flood-opacity="0" result="BackgroundImageFix" />
            <feColorMatrix
              in="SourceAlpha"
              type="matrix"
              values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
              result="hardAlpha"
            />
            <feOffset dx="0" dy="4" />
            <feGaussianBlur stdDeviation="1.33333" />
            <feComposite in2="hardAlpha" operator="out" k2="-1" k3="1" />
            <feColorMatrix
              type="matrix"
              values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"
            />
            <feBlend
              mode="normal"
              in2="BackgroundImageFix"
              result="effect_dropShadow_1"
            />
            <feBlend
              mode="normal"
              in="SourceGraphic"
              in2="effect_dropShadow_1"
              result="shape"
            />
          </filter>
          <clipPath id="clip9_684">
            <rect
              id="plus"
              width="21.000000"
              height="23.624998"
              fill="white"
              fill-opacity="0"
            />
          </clipPath>
        </defs>
        <rect
          id="plus"
          width="21.000000"
          height="23.624998"
          fill="#FFFFFF"
          fill-opacity="0"
        />
        <g clip-path="url(#clip9_684)">
          <g filter="url(#filter_2_116_dd)" />
          <path
            id="primary"
            d="M16.625 11.8125L4.375 11.8125L16.625 11.8125ZM10.5 4.92188L10.5 18.7031"
            stroke="#FFFFFF"
            stroke-opacity="1.000000"
            stroke-width="2.000000"
            stroke-linejoin="round"
            stroke-linecap="round"
          />
        </g>
      </svg>
    </button>
  </div>
</template>

<script setup>
import Task from "./Task.vue/";

defineEmits(["delete-task", "change-task", "toggle-component"]);
defineProps({
  taskName: {
    type: String,
    default: "",
  },
  tasks: {
    type: Array,
    default: () => [],
  },
});
</script>

<style scoped>
.todo {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: start;
  background: #d6d7ef;
}

.todo__button-toggle {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  right: 10%;
  bottom: 10%;
  background-color: #9395d3;
  border-radius: 50%;
  width: 70px;
  height: 70px;
  transition:
    box-shadow 0.2s ease-out,
    top 0.2s ease-out;

  @media (min-width: 500px) {
    right: 15%;
    bottom: 15%;
  }

  @media (min-width: 1024px) {
    right: 20%;
    bottom: 20%;
  }
}

.todo__button-toggle:hover {
  box-shadow: rgba(0, 0, 0, 0.45) 0 25px 20px -20px;
}

.todo__list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  list-style: none;
  padding-top: 40px;
  justify-content: center;
  align-items: center;
}

.todo__text {
  background-color: white;
  text-align: center;
  padding: 30px;
  margin-top: 100px;
  border-radius: 15px;
  color: #9395d3;
  font-weight: bold;
  font-size: 15px;

  @media (min-width: 500px) {
    max-width: 400px;
    font-size: 20px;
  }

  @media (min-width: 901px) {
    max-width: 600px;
    font-size: 30px;
  }
}
</style>
