/* eslint-disable space-before-function-paren */
<template>
  <q-page class="bg-grey-3 column">
      <div class="row q-pa-sm bg-primary">
        <q-input
          @keyup.enter='addTodo'
          v-model='newTodo'
          class='col'
          square
          filled
          bg-color='white'
          placeholder="ADD TODO"
          dense
        >
        <template v-slot:append>
          <q-btn
            @click='addTodo'
            round
            dense
            flat
            icon="add"
          />
        </template>
      </q-input>
      </div>
      <q-list
        class='bg-white'
        separated
        bordered
      >

      <q-item
        v-for='(task, index) in tasks'
        :key='index'
        @click='task.done = !task.done'
        :class="{ 'done bg-blue-1' : task.done }"
        clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class='no-pointer-events'
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if='task.done'
          side
        >
          <q-btn
            @click.stop='deleteTask(index)'
            flat
            round
            dense
            color="primary"
            icon="delete"
          />
        </q-item-section>
      </q-item>

    </q-list>
    <div
      v-if='!tasks.length'
      class='no-todos absolute-center'>
      <q-icon
        name='check'
        size='100px'
        color='primary'
      />
      <div class="text-h5 text-primary text-center">
        NO TODOS
      </div>
    </div>
  </q-page>
</template>

<script>

export default {
  data () {
    return {
      newTodo: '',
      tasks: []
    }
  },
  methods: {
    deleteTask (index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you wish to delete this TODO?',
        cancel: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('TODO deleted')
      })
    },
    addTodo () {
      this.tasks.push({
        title: this.newTodo,
        done: false
      })
      this.newTodo = ''
    }
  }
}
</script>

<style lang='scss'>
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
  .no-todos {
    opacity: 0.5;
  }
</style>
