<template>
    <div class="form-button">
        <button
            v-if="props.todoSelected"
            type="button"
            @click="updateHandler"
        >Update</button>

        <button
            v-else
            type="button"
            @click="storeHandler"
        > Create New </button>
    </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue';

const emit = defineEmits(['onStore', 'onUpdate']);

const props = defineProps({
    todoSelected: {
        type: Object,
        default: null,
    }
});
const storeHandler = () => {
    emit('onStore')
}

const confirmMassage = {
    update: 'Bạn thực sự muốn update ?'
}

const updateHandler = () => {
    if(confirm(confirmMassage.update)) {
        emit('onUpdate')
    }
}
</script>