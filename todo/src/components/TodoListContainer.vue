<template>
    
</template>

<script>
import { ref, readonly, provde } from 'vue'

export default {

    name: 'TodoListContainer',

    setup() {
        const todos = ref([]);
        provide('todos', readonly(todos))
        const initTodos = (init_todos) =>

    }




}


</script>
