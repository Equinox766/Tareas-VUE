<template>
  <div>
    <h1 class="display-4 text-center">Listado de tareas</h1>
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <div class="card mt-4">
          <div class="card-body">
            <div class="input-group">
              <input type="text" v-model="tarea"
              class="form-control form-control-lg" placeholder="Agregar Tarea"/>
              <div class="input-group-append">
                <button v-on:click="agregarTarea()"
                class="btn btn-success btn-lg">Agregar</button>
              </div>
            </div>
            <br>
            <h4 v-if="listTareas.length == 0" 
                class="text-center">No hay tareas para realizar
            </h4>
            <ul class="list-group">
                <li v-for="(tarea, index) of listTareas" :key="index" 
                class="list-group-item d-flex justify-content-between">
                    <span class="cursor"
                        v-bind:class="{'text-warning': tarea.estado}" 
                        v-on:click="editarTarea(tarea, index)">
                        <i v-bind:class="[tarea.estado ?  'text-success bi bi-check-circle-fill' : 'text-warning bi bi-exclamation-circle-fill']"></i>
                    </span>
                        <h3>{{tarea.nombre}}</h3>
                    <span class="text-danger cursor" v-on:click="eliminarTarea(index)">
                        <i class="bi bi-trash"></i>
                    </span>
                </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppTarea",
  data() {
    return {
        tarea: '',
        listTareas: []
    }
  },
  methods: {
    agregarTarea() {
        const tarea = {
            nombre: this.tarea,
            estado: false
        }
        this.listTareas.push(tarea);
        this.tarea = '';
    },
    eliminarTarea(index){
        this.listTareas.splice(index, 1)
    },
    editarTarea(tarea, index){
        this.listTareas[index].estado = !tarea.estado;
    }
  }
};
</script>

<style scoped>
.cursor{
    cursor: pointer;
}
</style>