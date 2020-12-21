<template>
  <div class="home">
    <v-text-field
    @click:append="addTask"
    @keyup.enter="task"
    v-model="newTaskTitle"
    class="pa-3"
    outlined
    label="Add Task"
    append-icon="mdi-plus"
    hide-details
    clerable
    ></v-text-field>
    <v-list
    flat class="pt-0"
    >
    <div v-for='task in tasks'
    :key="task.id">
      <v-list-item
      @click="doneTask(task.id)"
      :class="{'blue lighten-5': task.done}">

      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title 
          :class="{'text-decoration-line-through': task.done}">{{task.title}}</v-list-item-title>
        </v-list-item-content>

        <v-btn 
        @click.stop="deleteTask(task.id)"
        icon>
          <v-icon color="primary lighten-1">mdi-delete</v-icon>
        </v-btn>

      </template>
      <v-divider></v-divider>
    </v-list-item>
    <v-divider></v-divider>
    </div>
    </v-list>

       
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      newTaskTitle: '',
      tasks: [
      ]
    }
  },
  methods: {
    addTask(){
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false
      }
      this.tasks.push(newTask)
      this.newTaskTitle = ''
    },
    doneTask(id) {
       let task = this.tasks.filter(task =>task.id ===id)[0]
       task.done = !task.done
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id)
    }
  }
}
</script>
