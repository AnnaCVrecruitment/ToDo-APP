<template>
  <div class="task">
    <textarea
      :disabled="isReadonly"
      v-model="taskName"
      class="task__name"
      @keyup.esc="resetTask"
      rows="1"
      cols="20"
    >
    </textarea>
    <button
      class="task__edit-button"
      v-if="isReadonly"
      @click="changeReadonly(false)"
    >
      <svg
        fill="#9395d3"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          clip-rule="evenodd"
          d="m15.361 2.91158c1.2154-1.21544 3.186-1.21544 4.4015 0l1.3259 1.32595c1.2155 1.21544 1.2155 3.18607 0 4.40151l-12.44936 12.44936c-.58368.5837-1.37531.9116-2.20076.9116h-3.58946c-.46879 0-.84882-.38-.84882-.8488v-3.5895c0-.8254.32791-1.6171.91158-2.2007zm3.2011 1.20042c-.5525-.55248-1.4483-.55248-2.0007 0l-2.3263 2.32628 3.3266 3.32663 2.3263-2.32628c.5525-.55248.5525-1.44821 0-2.00069zm-2.2008 6.8533-3.3266-3.3266-8.9227 8.9227c-.26531.2653-.41436.6251-.41436 1.0003v2.7407h2.74064c.37521 0 .73504-.1491 1.00035-.4144z"
          fill="#9395d3"
          fill-rule="evenodd"
        />
      </svg>
    </button>
    <button class="saveTask" v-else @click="onSave">
      <svg
        fill="#9395d3"
        viewBox="-21 -21 682.66669 682.66669"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="m547.855469 0h-472.855469c-41.359375 0-75 33.640625-75 75v490c0 41.359375 33.640625 75 75 75h490c41.359375 0 75-33.640625 75-75v-472.855469zm-397.855469 50h187.5v140h-162.5c-13.785156 0-25-11.214844-25-25zm237.5 0h50v115c0 13.785156-11.214844 25-25 25h-25zm102.5 540h-340v-250h340zm100-25c0 13.785156-11.214844 25-25 25h-25v-300h-440v300h-25c-13.785156 0-25-11.214844-25-25v-490c0-13.785156 11.214844-25 25-25h25v115c0 41.359375 33.640625 75 75 75h237.5c41.359375 0 75-33.640625 75-75v-115h39.644531l62.855469 62.855469zm-150-125h-240v-50h240zm-87.5 100h-152.5v-50h152.5zm0 0"
        />
      </svg>
    </button>
    <button class="deleteTask" @click="$emit('delete-task')">
      <svg
        id="Layer_2"
        viewBox="0 0 32 32"
        xmlns="http://www.w3.org/2000/svg"
        fill="#9395d3"
      >
        <g>
          <path
            d="m28.50031 6.22144h-4.95685v-1.55463c0-2.02149-1.64533-3.66681-3.66681-3.66681h-7.7533c-2.02148 0-3.66681 1.64532-3.66681 3.66681v1.55463h-4.95685c-.80139 0-1.4516.65021-1.4516 1.4516 0 .80145.65021 1.45166 1.4516 1.45166h1.08099l1.66913 18.53735c.172 1.90332 1.74177 3.33795 3.65174 3.33795h12.1969c1.90997 0 3.47974-1.43463 3.65173-3.33795l1.66913-18.53735h1.08099c.80139 0 1.4516-.65021 1.4516-1.45166 0-.8014-.6502-1.4516-1.45159-1.4516zm-17.14057-1.55463c0-.42151.3421-.76361.76361-.76361h7.7533c.42151 0 .76361.3421.76361.76361v1.55463h-9.28052zm11.49854 22.73437c-.03589.39691-.36194.69556-.75983.69556h-12.1969c-.39789 0-.72394-.29865-.75983-.69556l-1.64538-18.27649h17.00732z"
          />
          <path
            d="m12.73669 24.92798c.80145 0 1.4516-.65021 1.4516-1.4516v-9.73132c0-.80139-.65015-1.4516-1.4516-1.4516-.80139 0-1.4516.65021-1.4516 1.4516v9.73132c.00001.80139.65021 1.4516 1.4516 1.4516z"
          />
          <path
            d="m19.26331 24.92798c.80139 0 1.4516-.65021 1.4516-1.4516v-9.73132c0-.80139-.65021-1.4516-1.4516-1.4516-.80145 0-1.4516.65021-1.4516 1.4516v9.73132c0 .80139.65014 1.4516 1.4516 1.4516z"
          />
        </g>
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";

const props = defineProps({
  taskName: {
    type: String,
    default: null,
  },
});
const emit = defineEmits(["delete-task", "change-task"]);
const isReadonly = ref(true);
const taskName = ref(props.taskName);

function changeReadonly(value) {
  isReadonly.value = value;
}

function onSave() {
  changeReadonly(true);
  emit("change-task", taskName.value);
}

function resetTask() {
  taskName.value = props.taskName;
  changeReadonly(true);
}
</script>

<style scoped>
.task__name {
  border: none;
  border-radius: 3px;
  outline: none;
  color: #9395d3;
  font-size: 15px;
  margin-left: 10px;
  font-weight: 600;
  resize: none;
  padding: 10px;

  @media (min-width: 400px) {
    font-size: 20px;
    padding: 5px 20px;
  }
}

.task__name:focus {
  border: 1px solid #747bff;
}

.task {
  display: flex;
  gap: 10px;
  align-items: center;
  color: #9395d3;
  padding: 10px;
  background-color: white;
  justify-content: center;
  border-radius: 15px;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.5);
  margin: 0 auto;
  max-width: 80%;
  font-weight: bolder;
  border: 1px solid transparent;

  @media (min-width: 900px) {
    width: 450px;
    min-height: 50px;
  }
}

.task:hover,
.task:active {
  border: 1px solid #747bff;
}

.deleteTask,
.task__edit-button,
.saveTask {
  background-color: transparent;
  padding: 5px;
  width: 40px;
  height: 40px;
}

.deleteTask:focus,
.deleteTask:hover,
.task__edit-button:focus,
.task__edit-button:hover,
.saveTask:focus,
.saveTask:hover {
  border: 1px solid #747bff;
}
</style>
