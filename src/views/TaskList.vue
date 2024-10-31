<template>
  <div class="container mt-4 text-light p-4 rounded">
    <h2 class="text-center mb-4">Lista de Tareas</h2>

    <div class="text-center mb-4">
      <button class="btn btn-outline-light" @click="fetchTasks">
        Cargar Tareas
      </button>
    </div>

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
              :class="task.completed ? 'bi bi-x-circle' : 'bi bi-check-circle'"
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
</template>

<script>
import axios from "axios";

export default {
  name: "TaskList",
  data() {
    return {
      tasks: [], // Almacenamiento local de las tareas traídas de la API
    };
  },
  methods: {
    // Llamada para obtener las tareas desde la API externa
    fetchTasks() {
      axios
        .get("https://dummyjson.com/todos")
        .then((response) => {
          this.tasks = response.data.todos;
        })
        .catch((error) => {
          console.log("Error al obtener las tareas", error);
        });
    },

    // Cambiar el estado de una tarea (completada/no completada)
    toggleTaskCompletion(task) {
      task.completed = !task.completed;
    },

    // Eliminar la tarea seleccionada
    deleteTask(task) {
      this.tasks = this.tasks.filter((t) => t.id !== task.id);
    },
  },
};
</script>

<style scoped>
h1 {
  color: #ffffff;
}

.task-list {
  color: #ffffff;
  padding: 20px;
}

.fs-5 {
  font-size: 1.25rem; /* Aumenta el tamaño de fuente */
}

.status-label {
  font-size: 1rem; /* Tamaño para el estado */
  text-align: left;
}

/* Fondo y colores para el modo oscuro */
.text-decoration-line-through {
  text-decoration: line-through;
}

.bg-secondary {
  background-color: #495057 !important;
}
</style>
