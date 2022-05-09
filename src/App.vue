<template>
  <div class="container">
    <div class="row">
      <div class="col mx-auto text-center">
        <div class="card p-4">
          <h4 class="text-secondary mt-4">TodoList</h4>
          <form class="mt-4" @submit.prevent="agregarNuevaTarea()">
            <div class="form-group row">
              <div class="col-9">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Ingresa una nueva tarea"
                  required
                  v-model="nuevaTarea"
                />
              </div>
              <div class="col-2">
                <button type="submit" class="btn btn-outline-secondary">
                  Agregar
                </button>
              </div>
            </div>
          </form>
          <h4 class="text-secondary mt-4">Tareas Pendientes</h4>
          <ul class="list-group">
            <li
              class="list-group-item"
              v-for="(tarea, $index) of tareasNuevas"
              :key="$index"
            >
              {{ $index + 1 }}: {{ tarea }}
              <div class="d-flex col-4 gap-1 mx-auto">
                <button @click="eliminarTarea($index)" type="button" class="btn btn-secondary">-</button>
                <!-- CON V-FOR -->
                <select @change="moverTarea(tarea, $index, $event)" class="form-select form-select-sm" aria-label=".form-select-sm multiple select">
                  <option value="En proceso">En proceso</option>
                  <option value="Completada">Completada</option>
                </select>
              </div>
            </li>
          </ul>
          <h4 class="text-secondary mt-4">Tareas Terminadas</h4>
          <ul class="list-group">
            <li
              class="list-group-item"
              v-for="(tarea, $index) of tareasCompletadas"
              :key="$index"
            >
              {{ $index + 1 }}: {{ tarea }}
               <div class="d-flex col-4 gap-1 mx-auto">
                <button @click="eliminarTareaCompletada($index)" type="button" class="btn btn-secondary">-</button>
                <select @change="moverTarea(tarea, $index, $event)" class="form-select form-select-sm" aria-label=".form-select-sm multiple select">
                  <option value="Completada">Completada</option>
                  <option value="En proceso">En proceso</option>
                </select>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    nuevaTarea: "",
    tareasNuevas: [],
    tareasCompletadas: [],
  }),
  methods: {
    agregarNuevaTarea() {
      this.tareasNuevas.unshift(this.nuevaTarea);
      this.nuevaTarea = "";
    },
    eliminarTarea(index) {
      this.tareasNuevas.splice(index, 1);
    },
    eliminarTareaCompletada(index) {
      this.tareasCompletadas.splice(index, 1)
    },
    moverTarea(tarea, index, event){
      console.log(this.estadoTarea)
      if (event.target.value == "Completada") {
        this.tareasCompletadas.push(tarea);
        this.tareasNuevas.splice(index, 1);
        console.log("dentro del else");
      } else if (event.target.value == "En proceso") {
        console.log("dentro del else");
        this.tareasNuevas.push(tarea);
        this.tareasCompletadas.splice(index, 1);
      }
    }
  },
};
</script>

<style></style>