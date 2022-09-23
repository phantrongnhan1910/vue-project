<template>
    <div class="form-input">
        <input 
            type="text"
            :value="todoInput"
            @input="inputHandler"
        >
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits(['onInput']);

const props = defineProps({
    todoInput: {
        type: String,
        default: '',
    }
});

const inputHandler = (e) => {
    const value = e.target.value;
    emit('onInput', value)
}
</script>
<style>

</style>