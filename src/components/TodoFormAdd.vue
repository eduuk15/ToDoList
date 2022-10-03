<template>


    <div class="absolute w-96">
        <TodoAlertSuccess
            id="alert"
            v-if="adicionado"
        />
    </div>
    <form
        @submit.stop.prevent="addTodo"
        class="flex items-center px-4 bg-gray-900 h-15 rounded-sm border-l-2 border-green-400 mb-3">
                <input
                    v-model="title"
                    placeholder="Adicione um novo item ..."
                    type="text"
                    class="bg-gray-900 placeholder-gray-500 text-gray-500 font-light focus:outline-none block w-full appearance-none leading-normal py-3 pr-3"
                >

                <button
                    class="text-green-400 text-xs font-semibold focus:outline-none"
                    type="submit"
                >
                    ADICIONAR
                </button>
    </form>
</template>

<script>
import TodoAlertSuccess from './TodoAlertSuccess.vue'
export default {
    components: {
        TodoAlertSuccess,
    },
    data() {
        return {
            title: '',
            adicionado: false
        }
    },
    methods: {
        addTodo() {
            if (!this.title) {
                return false;
            }
            this.$store.dispatch('addTodo', {
                title: this.title,
                completed: false
            }).finally(() => {
                this.title = ''
                this.adicionado = true
            })

            setTimeout(() => {
                this.adicionado = false
            }, 1500)
        }
    }
}
</script>
