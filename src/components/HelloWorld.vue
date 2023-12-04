<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12" md="8">
        <h1 class="text-h5">Lista de tareas</h1>
        <v-btn @click="addTask" color="primary">Agregar tarea</v-btn>

        <v-row v-if="agregar" class="mt-2">
          <v-col cols="12">
            <v-text-field v-model="newTask" label="Nueva Tarea"></v-text-field>
          </v-col>
          <v-col cols="12" class="mt-2">
            <v-btn @click="addNewTask" color="success">Guardar</v-btn>
          </v-col>
        </v-row>

        <v-list class="mt-4">
          <v-list-item-group v-if="tasks.length > 0">
            <v-list-item v-for="(task, index) in tasks" :key="index">
              <v-list-item-content>
                <v-list-item-title v-if="isEditing(index)">
                  <v-text-field v-model="tasks[index]" outlined></v-text-field>
                  <v-btn @click="updateTaskOk" color="success" >Guardar</v-btn>
                </v-list-item-title>
                <v-list-item-title v-else>
                  {{ task }}
                </v-list-item-title>
              </v-list-item-content>

              <v-list-item-action>
                <v-btn @click="updateTask(index)" icon>
                  <v-icon>mdi-pencil</v-icon>
                </v-btn>
              </v-list-item-action>

              <v-list-item-action>
                <v-btn @click="deleteTask(index)" icon>
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list-item-group>
          <v-list-item v-else>
            <v-list-item-content>No hay tareas</v-list-item-content>
          </v-list-item>
        </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      tasks: ["Tarea 1", "Tarea 2", "Tarea 3"],
      newTask: "",
      agregar: false,
      editingIndex: null
    };
  },
  methods: {
    addTask() {
      this.newTask = "";
      this.agregar = true;
    },
    addNewTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push(this.newTask);
        this.newTask = "";
        this.agregar = false;
      }
    },
    updateTask(index) {
      this.editingIndex = index;
    },
    updateTaskOk() {
      this.editingIndex = null;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.editingIndex = null;
    },
    isEditing(index) {
      return this.editingIndex === index;
    }
  },
  mounted() {}
};
</script>
