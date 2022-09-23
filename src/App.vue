<template>
  <div class="container">
    <app-title 
      class="appTitle"
      :title="App_Title" 
    />
    <app-content class="appContent"/>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import AppTitle from './components/AppTitle.vue';
import AppContent from './components/AppContent.vue';

const App_Title = 'My todo Application';
</script>

<style>
.container {
  width: 900px;
  margin: 0 auto;
  border: 1px solid #ccc;
}
.appTitle {
  text-align: center;
  margin: 10px;
}
.appContent {
  border: 1px solid #ccc;
  margin: 10px;
}
</style>