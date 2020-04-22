<template>
  <q-page class="bg-grey-3 column">
    <div-row class="q-pa-sm bg-primary" :class="$q.dark.isActive ? 'bg-grey-10' :'bg-primary'">
       <q-input class="col" @keyup.enter="addTask" square filled v-model=" newTask" label="Adicionar Tarefa" :class="$q.dark.isActive ? 'bg-grey-10' :'bg-white'">
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>
      </q-input>
    </div-row>
    <q-list class="bg-white separator bordered">

      <q-item v-for="(task, index) in tasks" :key="task.title" @click="task.done = !task.done" :class="{ 'done bg-blue-1' : task.done }" clickable v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="task.done" class="no-pointer-events" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
         <q-item-section
         v-if="task.done"
         side>
          <q-btn flat round color="primary" dense @click.stop="deleteTask(index)" icon="delete" />
        </q-item-section>
      </q-item>

    </q-list>
    <div v-if="!tasks.lenght" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary"/>
      <div class="text-h5 text-primary text-center">
        Vazio
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      newTask: '',
      tasks: [
      ]
    }
  },
  methods: {
    deleteTask (index) {
      this.$q.dialog({
        title: 'Confirmar',
        message: 'Deseja mesmo excluir?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Tarefa Deletada')
      })
    },
    addTask () {
      this.tasks.push({
        title: this.newTask,
        done: false
      })
      this.newTask = ''
    }
  }

}
</script>

<style lang="scss">
.done{
  .q-item__label{
  text-decoration: line-through;
  color: #bbb;
  }
}
.no-tasks{
    opacity: 0.5;
  }
</style>
