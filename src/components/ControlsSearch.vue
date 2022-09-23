<template>
    <div class="Controls-Search">
        <input 
            type="text"
            :value="searchInput"
            @input="inputSearch"
        >
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits(['onSearch']);
const props = defineProps({
    searchInput: {
        type: String,
        default: '',
    }
});

const inputSearch = (e) => {
    const value = e.target.value;
    emit('onSearch', value)
}
</script>
<style>
.Controls-Search {
    margin-right: 10px;
}
</style>