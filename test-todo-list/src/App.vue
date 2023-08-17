<template>
  <div>
    <AddTask @task-added="addTask" />

    <ul>
      <li v-for="task in tasks" :key="task.id">
        <div class="editing-container">
          <template v-if="task.editing">
            <input v-model="task.text" @keyup.enter="saveTask(task)" @keyup.esc="cancelEdit(task)" />
            <button @click="saveTask(task)" class="save-button">Сохранить</button>
            <button @click="cancelEdit(task)" class="cancel-button">Отмена</button>
            <button @click="deleteTask(task)">Удалить</button>
            <input type="checkbox" v-model="task.completed" class="checkbox" />
          </template>
          <template v-else>
            <span :class="{ 'completed-task': task.completed }">{{ task.text }}</span>
            <button @click="editTask(task)">Редактировать</button>
          </template>
        </div>
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
  created() {
    this.loadFromLocalStorage();
  },
  methods: {
    addTask(newTaskText) {
      const newTask = { id: Date.now(), text: newTaskText, editing: false, completed: false };
      this.tasks.push(newTask);
      this.saveToLocalStorage();
    },
    editTask(task) {
      task.editing = true;
    },
    saveTask(task) {
      task.editing = false;
      this.saveToLocalStorage();
    },
    cancelEdit(task) {
      task.editing = false;
      this.saveToLocalStorage();
    },
    completedTask(task) {
      task.editing = false;
      this.saveToLocalStorage();
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter(t => t.id !== task.id);
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      let myStorage = window.localStorage;
      myStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    loadFromLocalStorage() {
      const storedTasks = window.localStorage.getItem('tasks');
      if (storedTasks) {
        this.tasks = JSON.parse(storedTasks);
      }
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
  border-bottom: 4px solid black;
}

button {
  font-size: 24px;
  border-radius: 4px;
  cursor: pointer;
}

input {
  font-size: 24px;
}

span {
  font-size: 24px;
}

.checkbox {
  display: block;
  width: 40px;
}

.editing-container {
  display: flex;
  justify-content: space-between;
}

.completed-task {
text-decoration: line-through;
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




