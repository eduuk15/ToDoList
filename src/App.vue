<template>
    <div class="px-3 py-10 md:px-10">
        <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
          <div class="flex justify-center text-green-400 font-semibold text-title">
              To Do List (Lista de Tarefas)
          </div>

          <TodoSpinner v-if="loading"/>

          <template v-else>
            <TodoFormAdd :alert="alert" @changeAlert="changeAlert($event)"/>
            <TodoItems v-if="$store.state.todos.length"/>
            <TodoEmpty v-else/>
            <TodoAlerts v-if="alert === 'adicionou'"/>
          </template>

        </div>
    </div>
</template>

<script>

import TodoSpinner from './components/TodoSpinner.vue'
import TodoFormAdd from './components/TodoFormAdd.vue'
import TodoItems from './components/TodoItems.vue'
import TodoEmpty from './components/TodoEmpty.vue'
import TodoAlerts from './components/TodoAlerts.vue'

export default {
  name: 'App',
  components: {
    TodoSpinner,
    TodoFormAdd,
    TodoItems,
    TodoEmpty,
    TodoAlerts
  },
  data() {
    return {
      loading: false,
      alert: ''
    }
  },
  created() {
    this.loading = true
    this.$store.dispatch('getTodos').finally(() => {
      this.loading = false
    })
  },
  methods: {
    changeAlert(alert) {
      this.alert = alert
    }
  },
}
</script>
