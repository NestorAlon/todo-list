<template>
  <div class="container mt-4 text-light p-4 rounded">
    <h2 class="text-center mb-4">Gestor de Tareas</h2>

    <div class="add-task-container mb-4">
      <h3>Añadir Tarea</h3>
      <div class="input-group">
        <input
          v-model="newTask"
          @keyup.enter="addTask"
          placeholder="Añadir nueva tarea"
          class="task-input"
        />
        <button @click="addTask" class="add-button">Añadir</button>
      </div>
    </div>

    <div class="task-list">
      <h3 class="text-center mb-4">Lista de Tareas</h3>
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
import axios from "axios";

export default {
  name: "CombinedView",
  data() {
    return {
      tasks: [], // Almacenamiento local de las tareas
      newTask: "", // Campo de entrada para la nueva tarea
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
    // Método para añadir una nueva tarea
    addTask() {
      if (this.newTask.trim() === "") return;

      const newTask = {
        todo: this.newTask,
        completed: false,
        id: Date.now(), // Asigna un ID único
      };

      this.tasks.unshift(newTask); // Añadir la nueva tarea al inicio de la lista
      this.newTask = ""; // Limpiar el campo de entrada después de agregar
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
  mounted() {
    // Cargar tareas al montar el componente
    this.fetchTasks();
  },
};
</script>

<style scoped>
h2 {
  color: #ffffff;
}
h3 {
  color: #d1d5db;
}
.add-task-container {
  margin-bottom: 20px;
}
.input-group {
  display: flex;
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
.fs-5 {
  font-size: 12.5px;
}
.status-label {
  font-size: 15px;
  text-align: left;
}
.text-decoration-line-through {
  text-decoration: line-through;
}
.bg-secondary {
  background-color: #495057 !important;
}
</style>
