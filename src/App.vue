<template>
  <div class="todo-container">
    <h1>ToDo List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.name }}</span>
        <button @click="toggleComplete(index)">✔️</button>
        <button @click="editTask(index)">✍</button>
        <button @click="deleteTask(index)">🗑</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        { name: 'Sample Task 1', completed: false },
        { name: 'Sample Task 2', completed: true }
      ]
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ name: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    toggleComplete(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    editTask(index) {
      const editedTask = prompt("Edit task:", this.tasks[index].name);
      if (editedTask !== null && editedTask.trim()) {
        this.tasks[index].name = editedTask;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped lang="scss">
.todo-container {
  max-width: 400px;
  margin: 0 auto;
  text-align: center;

  h1 {
    font-size: 24px;
    margin-bottom: 20px;
  }

  input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  .task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #eee;
    
    button {
      background: none;
      border: none;
      cursor: pointer;
      font-size: 16px;
    }

    button:hover {
      color: #007BFF;
    }

    button:nth-child(2):hover {
      color: #28a745;
    }

    button:nth-child(3):hover {
      color: #ffc107;
    }

    button:nth-child(4):hover {
      color: #dc3545;
    }
  }
}
</style>
