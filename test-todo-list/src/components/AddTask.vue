<template>
  <div class="addTask">
    <input v-model="newTaskText" placeholder="Enter task" class="input" maxlength="100" />
    <button @click="addTask">Add</button>
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
    font-size: 20px;
  }
</style>