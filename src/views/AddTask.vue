<template>
  <div class="container">
    <h2>Añadir Tarea</h2>
    <div class="input-group">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Añadir nueva tarea"
        class="task-input"
      />
      <button @click="addTask" class="add-button">Añadir</button>
    </div>

    <div v-if="tasks.length > 0" class="task-list">
      <ul class="list-group">
        <li
          v-for="task in tasks"
          :key="task.id"
          class="list-group-item d-flex justify-content-between align-items-center bg-secondary text-light mb-3 rounded p-3"
        >
          <div class="d-flex flex-column">
            <span
              :class="{
                'text-decoration-line-through text-muted': task.completed,
              }"
              class="fs-5 fw-bold"
            >
              {{ task.todo }}
            </span>

            <small
              :class="task.completed ? 'text-success' : 'text-warning'"
              class="status-label"
            >
              {{ task.completed ? "Completada" : "Pendiente" }}
            </small>
          </div>

          <div>
            <button
              class="btn btn-outline-light btn-sm me-2"
              @click="toggleTaskCompletion(task)"
            >
              <i
                :class="
                  task.completed ? 'bi bi-x-circle' : 'bi bi-check-circle'
                "
              ></i>
            </button>
            <button
              class="btn btn-outline-danger btn-sm"
              @click="deleteTask(task)"
            >
              <i class="bi bi-trash"></i>
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      newTask: "", // Campo de entrada para la nueva tarea
      tasks: [], // Lista de tareas locales
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() === "") return;

      const newTask = {
        todo: this.newTask,
        completed: false,
        id: Date.now(),
      };

      // Añadir la nueva tarea al inicio de la lista
      this.tasks.unshift(newTask);
      this.newTask = ""; // Limpiar el campo de entrada después de agregar
    },

    // Elimina una tarea específica de la lista
    deleteTask(task) {
      this.tasks = this.tasks.filter((t) => t.id !== task.id);
    },

    // Cambia el estado de la tarea entre completada y no completada
    toggleTaskCompletion(task) {
      task.completed = !task.completed;
    },
  },
};
</script>

<style scoped>
h2 {
  color: #ffffff;
  margin-bottom: 20px;
}
.container {
  margin: 40px auto;
}

.input-group {
  display: flex;
  margin-bottom: 10px;
}

.task-input {
  flex-grow: 1;
  padding: 8px;
  margin-right: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-button {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

.task-list {
  margin-top: 20px;
}

.list-group-item {
  font-weight: 600;
  color: #ffffff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.text-decoration-line-through {
  text-decoration: line-through;
  color: gray;
}
</style>
