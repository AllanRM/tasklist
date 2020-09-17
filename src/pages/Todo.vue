<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        class="col"
        square
        filled
        placeholder="Adicionar tarefa"
        dense
        bg-color="white"
        @keyup.enter="addTask"
        >
        <template v-slot:append>
          <q-btn
            round
            dense
            flat
            icon="add"
            @click="addTask"/>
        </template>
      </q-input>
    </div>

    <q-list class="bg-white" separator bordered>
      <q-item
        v-for="(task, index) in tasks" :key="task.title"
        v-ripple
        clickable
        :class=" {'done bg-blue-1' : task.done}"
        @click="task.done = !task.done">
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primaty" class="no-pointer-events"/>
        </q-item-section>
        <q-item-section>
          <q-item-label> {{task.title}} </q-item-label>
        </q-item-section>
        <q-item-section v-if="!task.done" side>
            <q-btn
              dense
              flat
              round
              color="primary"
              icon="delete"
              @click.stop="deleteTask(index)"
            />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="notask absolute-center">
      <q-icon name="check" size="300px" color="primary" class="justify-center" />
      <div class="text-h5 text-primary text-center">Nenhuma tarefa cadastrada</div>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      newTask: '',
      tasks: []
    }
  },
  methods: {
    addTask () {
      this.tasks.push(
        {
          done: false,
          title: this.newTask
        }
      )
      this.newTask = ''
    },
    deleteTask (index) {
      this.$q.dialog({
        title: 'Excluir',
        message: 'Deseja realmente eliminar esta tarefa?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Tarefa excluida')
      })
    }
  }

}
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }

  .notask {
    opacity: 0.2;
  }
</style>
