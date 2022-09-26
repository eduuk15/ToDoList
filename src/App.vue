<template>
    <div class="px-3 py-10 md:px-10">
        <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
          <div class="flex justify-center text-green-400 font-semibold text-title">
              To Do List (Lista de Tarefas)
          </div>

          <TodoSpinner v-if="loading"/>

          <template v-else>
            <TodoFormAdd />
            <TodoItems v-if="$store.state.todos.length" />
            <TodoEmpty v-else/>
            <TodoAlertSuccess v-if="todosLength > todosLengthOriginal"/>
            <TodoAlertRemove v-if="todosLength < todosLengthOriginal"/>
          </template>

        </div>
    </div>
</template>

<script>

import TodoSpinner from './components/TodoSpinner.vue'
import TodoFormAdd from './components/TodoFormAdd.vue'
import TodoItems from './components/TodoItems.vue'
import TodoEmpty from './components/TodoEmpty.vue'
import TodoAlertSuccess from './components/TodoAlertSuccess.vue'
import TodoAlertRemove from './components/TodoAlertRemove.vue'

export default {
  name: 'App',
  components: {
    TodoSpinner,
    TodoFormAdd,
    TodoItems,
    TodoEmpty,
    TodoAlertSuccess,
    TodoAlertRemove
  },
  data() {
    return {
      loading: false,
      todosLengthOriginal: '',
      todosLength: ''
    }
  },
  created() {
    this.loading = true
    this.$store.dispatch('getTodos').finally(() => {
      this.loading = false
    })
    this.todosLengthOriginal = this.$store.state.todos.length;
    console.log('orig 1', this.todosLengthOriginal);
  },
  updated() {
    this.todosLength = this.$store.state.todos.length;
    console.log(this.todosLength);
    console.log('orig 2', this.todosLengthOriginal);
  }
}
</script>
