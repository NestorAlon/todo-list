<template>
  <nav>
    <nav class="navbar navbar-expand-lg custom-nav">
      <div class="container">
        <img class="img-logo" alt="Vue logo" src="../assets/logo.png" />
        <a class="navbar-brand" href="/"
          ><i class="icono bi bi-journal-check"></i>Gestor de Tareas</a
        >
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a
                class="nav-link custom-hover"
                aria-current="page"
                href="/addtask"
                ><i class="icono bi bi-plus-circle"></i>Agregar
                <Tarea:r></Tarea:r
              ></a>
            </li>
            <li class="nav-item">
              <a class="nav-link custom-hover" href="/tasklist"
                ><i class="icono bi bi-list-check"></i>Lista de Tareas</a
              >
            </li>
            <li class="nav-item">
              <a class="nav-link custom-hover" href="/combinedview"
                ><i class="icono bi bi-grid"></i>Vista Combinada</a
              >
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
};
</script>

<style scoped>
.navbar-brand {
  font-size: 20px;
  text-transform: uppercase;
  font-weight: 700;
}

.img-logo {
  max-width: 50px;
  margin-right: 3rem;
}

.icono {
  color: dark;
  margin-right: 10px;
  font-size: 20px;
  vertical-align: middle;
}

.nav-link {
  color: #d1d5db;
  font-size: 20px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 600;
  margin-right: 10px;
}

.custom-nav {
  background-color: #155e75;
}

.custom-hover {
  transition: background-color 0.3s ease;
}

.custom-hover:hover {
  color: #2dd4bf;
}

.navbar-brand {
  color: #ffffff;
}
</style>
