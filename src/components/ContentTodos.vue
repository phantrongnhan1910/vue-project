<template>
    <div class="Content-Todos">
        <template v-if="props.todos.length > 0">
            <todos-item 
            v-for="(todo,index) in props.todos"
            :key="index"
            :id="todo.id"
            :title="todo.title"
            @on-del="delHandler"
            @on-edit="editHandler"
        />   
        </template>
        <div v-else> TODO IS EMPTY!</div>
    </div>
</template>

<script setup>
import TodosItem from './TodosItem.vue';
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits(['onDel', 'onEdit']);

const props = defineProps({
    todos: {
        type: Array,
        default: [],
    }
});

const delHandler = (id) => {
    emit('onDel', id)
}
const editHandler = (id) => {
    emit('onEdit', id)
}
</script>
<style>
    .Content-Todos {
        border: 1px solid #ccc;
        padding: 5px;
    }
</style>