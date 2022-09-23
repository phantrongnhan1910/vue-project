<template>
    <div class="Todos-Item">
        <div class="Todos-Item_title">{{ title }}</div>
        <div class="Todos-Item_wrapper">
            <div class="Todos-Item_edit">
                <button
                    type="button"
                    @click="editHandler"
                >EDIT</button>
            </div>
            <div class="Todos-Item_delete">
                <button
                    type="button"
                    @click="delHandler"
                >DELETE</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
import FormButton from './FormButton.vue';

const emit = defineEmits(['onDel', 'onEdit']);

const props = defineProps({
    id: {
        type: String,
        required: true,
    },
    title: {
        type: String,
        required: true,
    }
});

const confirmMassage = {
    del: 'Bạn thực sự muốn xóa không ?'
}

const delHandler = () => {
    if(confirm(confirmMassage.del)) {
        emit('onDel', props.id);
    }
}

const editHandler = () => {
    emit('onEdit', props.id)
}
</script>
<style>
    .Todos-Item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin: 10px;
        background-color: rgb(233, 212, 212);
    }
    .Todos-Item_wrapper {
        display: flex;
    }
    
</style>