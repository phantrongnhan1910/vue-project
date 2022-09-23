<template>
    <div class="Content-Controls"> 
        <controls-search 
            :search-input="searchInput"
            @on-search="inputSearch"
        />
    </div>
</template>

<script setup>
import ControlsSearch from './ControlsSearch.vue';
import { defineProps, defineEmits } from 'vue';


const emit = defineEmits(['onSearch']);
const props = defineProps({
    searchInput: {
        type: String,
        default: '',
    }
});

const inputSearch = (value) => {
    emit('onSearch', value)
}
</script>
<style>
.Content-Controls {
    display: flex;
}
</style>