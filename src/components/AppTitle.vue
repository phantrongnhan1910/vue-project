<template>
    <h1>{{ title }}</h1>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    title: {
        type: String,
        default: 'My Todo'
    }
})
</script>