<script setup lang="ts">
import { ref } from 'vue';

const root = document.querySelector(':root');

const currentTheme = ref(localStorage.getItem('theme') || 'dark-theme');
if (currentTheme.value === 'light-theme') root?.classList.add('light-theme');

function changeTheme()
{
  if (root){
    root.classList.toggle('light-theme');

    currentTheme.value = root.classList.contains('light-theme') ? 'light-theme' : 'dark-theme';
    localStorage.setItem('theme', currentTheme.value);
  }
}
</script>
<template>
  <button @click="changeTheme()">
    {{ currentTheme == 'light-theme' ? '🌑' : '☀️'}}
  </button>
</template>
<style scoped>
    button {
        padding: 20px 20px;
        
        position: absolute;
        top: 0px;
        right: 0px;
    }
</style>