<template>
  <v-container>
    <v-row>
      <v-col aling="center" col="6"  class="text-center">
        <h1>Añadir tareas</h1>
        <v-text-field
          v-model="task"
          label="Nueva tarea"
          required
        ></v-text-field>
        <v-container>
          <v-row>
            <v-col>
              <v-btn @click="add_task" class="ma-2" outlined color="blue">
                Añadir tarea
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
      <v-col col="6"  class="text-center">
        <h1>Lista de tareas</h1>
        <v-simple-table>
          <template v-slot:default>
            <thead>
          <tr>
            <th class="text-center">Nombre</th>
            <th class="text-center">Terminar</th>
            <th class="text-center">Eliminar</th>
            <th class="text-center">Editar</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(t,index) in all_task" :key="index" v-bind:style="t.done==true?'color:green':'color:red'">
            <td>{{t.name}}</td>
            <td><v-btn
              color="green"
              fab
              small
              dark
              @click="check_task(index)"
            >
              <v-icon>mdi-check</v-icon>
            </v-btn></td>
            <td><v-btn
              color="red"
              fab
              small
              dark
              @click="delete_task(index)"
            >
              <v-icon>mdi-delete</v-icon>
            </v-btn></td>
            <td><v-btn
              color="primary"
              fab
              small
              dark
              @click="dialog=true"
            >
              <v-icon>mdi-pencil</v-icon>
            </v-btn></td>
            <v-dialog
      v-model="dialog"
      max-width="290"
    >
      <v-card>
        <h3>Editar tarea</h3>
        <v-text-field
          v-model="t.name"
          required
        ></v-text-field>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Editar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
          </tr>
          </tbody>
          </template>
        </v-simple-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    task: '',
    all_task: [],
    dialog: false,
    edit_task: ''
  }),
  methods: {
    add_task () {
      if (this.task !== '') {
        const taskNew = {
          name: this.task,
          done: false
        }
        this.all_task.push(taskNew)
        this.task = ''
        console.log(this.all_task)
      }
    },
    delete_task (index) {
      this.all_task.splice(index, 1)
    },
    check_task (index) {
      this.all_task[index].done = !this.all_task[index].done
    }
  }
}
</script>
