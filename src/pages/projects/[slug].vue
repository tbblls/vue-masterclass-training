<script setup lang="ts">
const route = useRoute()
</script>

<template>
  <div>
    <h1>Project name: {{ route.params?.slug }}</h1>
    <RouterLink to="/projects/">Projects</RouterLink>
  </div>
</template>
