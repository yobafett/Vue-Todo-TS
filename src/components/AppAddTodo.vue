<template>
  <section class="add-todo">
    <button
      v-if="!isFormVisible"
      class="add-todo__show-form-button"
      @click="showForm"
    >
      <i class="bi bi-plus-lg"></i>
    </button>

    <form
      v-else
      class="add-todo__form"
      @submit.prevent="addTodo"
    >
      <button
        class="close-button"
        type="button"
      >
        <i
          class="bi bi-x"
          @click="closeForm"
        ></i>
      </button>
      <div class="text-input text-input--focus">
        <input
          class="input"
          v-model="todoText"
        />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Todo from '@/types/Todo';

interface State {
  isFormVisible: boolean;
  todoText: string;
}

export default defineComponent({
  name: 'AppAddTodo',
  data(): State {
    return {
      isFormVisible: false,
      todoText: '',
    };
  },
  methods: {
    showForm() {
      this.isFormVisible = true;
    },
    closeForm() {
      this.isFormVisible = false;
    },
    addTodo() {
      this.$emit('addTodo', {
        id: Date.now(),
        text: this.todoText,
        completed: false
      });
      this.todoText = '';
    },
  },
  emits: {
    addTodo: (todo: Todo) => todo,
  },
});
</script>
