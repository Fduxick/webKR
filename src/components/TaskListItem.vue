<template>
  <li class="task-item">
    <div :class="task.closed ? 'task-completed-wrapper' : ''">
      <div :class="task.closed ? 'task-completed' : ''"></div>
    </div>
    <div>
      <p class="task-created">start: {{ task.created }}</p>
      <p class="task-created">end: {{ task.closed ? task.closed : "" }}</p>
    </div>
    <textarea
      class="task-textarea"
      :value="task.text"
      @input="handleTextAreaChange"
    ></textarea>

    <select
      v-if="categories.length > 0"
      @change="handleSelectChange"
      class="task-select"
    >
      <option
        v-for="categorie in categories"
        :key="categorie.id"
        :value="categorie.id"
        :selected="categorie.id === task.categorie"
      >
        {{ categorie.type }}
      </option>
    </select>

    <button @click="handleBtnCompleteClick(task)" class="task-btn">done</button>

    <button @click="handleBtnDeleteClick(task)" class="task-btn del">X</button>
  </li>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
  },

  computed: {
    categories() {
      return this.$store.getters.categories;
    },
  },

  methods: {
    handleTextAreaChange(e) {
      const taskToUpdate = { ...this.task, text: e.target.value };

      this.$store.dispatch("updateTask", taskToUpdate);
    },

    handleSelectChange(e) {
      const taskToUpdate = {
        ...this.task,
        categorie: Number(e.target.value),
      };

      this.$store.dispatch("updateTask", taskToUpdate);
    },

    handleBtnDeleteClick(data) {
      this.$store.dispatch("deleteTask", data);
    },

    handleBtnCompleteClick() {
      if (!this.task.closed) {
        const d = new Date();

        const datestring =
          ("0" + d.getDate()).slice(-2) +
          "." +
          ("0" + (d.getMonth() + 1)).slice(-2) +
          " " +
          ("0" + d.getHours()).slice(-2) +
          ":" +
          ("0" + d.getMinutes()).slice(-2);

        const taskToUpdate = {
          ...this.task,
          closed: datestring,
        };

        this.$store.dispatch("updateTask", taskToUpdate);
      }
    },
  },
};
</script>
