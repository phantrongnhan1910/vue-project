<template>
    <div class="content-Form">
        <div class="content-Form_Top">
            <form-toggle    
                :is-show-form="isShowForm"
                @on-toggle="toggleHandler"
            />
        </div>
        <div class="content-Form_Bottom">
            <template v-if="props.isShowForm">
                <form-input 
                    :todo-input="todoInput"
                    @on-input="inputHandler"
                />
                <form-button 
                    :todo-selected="todoSelected"
                    @on-store="storeHandler"
                    @on-update="updateHandler"
                />
            </template>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
import FormToggle from './FormToggle.vue';
import FormInput from './FormInput.vue';
import FormButton from './FormButton.vue';

const emit = defineEmits(['onToggle', 'onInput', 'onStore', 'onUpdate']);

const props = defineProps({
    isShowForm: {
        type: Boolean,
        default: false,
    },
    todoInput: {
        type: String,
        default: '',
    },
    todoSelected: {
        type: Object,
        default: null,
    }
});

const toggleHandler = () => {
    emit('onToggle');
}

const inputHandler = (value) => {
    emit('onInput', value)
}
const storeHandler = () => {
    emit('onStore')
}

const updateHandler = () => {
    emit('onUpdate')
}

</script>
<style>
.content-Form_Bottom {
    display: flex;
}
</style>