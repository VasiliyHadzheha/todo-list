<template>
  <div>
    <AddTask @task-added="addTask" />
    
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <template v-if="task.editing">
          <input v-model="task.text" @keyup.enter="saveTask(task)" @keyup.esc="cancelEdit(task)" />
          <button @click="saveTask(task)" class="save-button">Сохранить</button>
          <button @click="cancelEdit(task)" class="cancel-button">Отмена</button>
        </template>
        <template v-else>
          {{ task.text }}
          <button @click="editTask(task)">Редактировать</button>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
import AddTask from '@/components/AddTask.vue';

export default {
  components: {
    AddTask
  },
  data() {
    return {
      tasks: []
    };
  },
  methods: {
    addTask(newTaskText) {
      this.tasks.push({ id: Date.now(), text: newTaskText, editing: false });
    },
    editTask(task) {
      task.editing = true;
    },
    saveTask(task) {
      task.editing = false;
    },
    cancelEdit(task) {
      task.editing = false;
    }
  }
};
</script>



<style>
  body {
    margin: 0;
    padding: 60px;
    margin: 0 auto;
    font-family: WorkSans-Medium;
    max-width: 1440px;
    background-color: gainsboro;
    /* background-attachment: fixed; */
    display: flex;
    justify-content: center;
    align-items: center;
  }

  p {
    font-size: 24px;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  li {
    list-style-type: none;
    padding: 4px;
    margin: 4px;
    border: 2px solid black;
  }

  button {
    border-radius: 4px;
  }


  .task-list {
    margin: 0;
    padding: 0;
  }

  #app {
    width: 1400px;
    height: 700px;
    display: flex;
    justify-content: center;
    background-color: blanchedalmond;
  }

  @font-face {
    font-family: WorkSans-Medium;
    src: url(/fonts/WorkSans-Medium.ttf);
  }
</style>




