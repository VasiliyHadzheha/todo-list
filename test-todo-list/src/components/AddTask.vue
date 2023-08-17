<template>
  <div class="addTask">
    <h1>TODO LIST</h1>
    <input v-model="newTaskText" placeholder="Введите задачу" class="input" maxlength="100" />
    <button @click="addTask">Добавить</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTaskText: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTaskText.trim() !== '') {
        this.$emit('task-added', this.newTaskText);
        this.newTaskText = '';
      }
    }
  }
};
</script>

<style>
  .addTask {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .input {
    margin: 15px;
    width: 300px;
    height: 30px;
    font-size: 24px;
  }
</style>