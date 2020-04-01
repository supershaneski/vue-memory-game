<template>
  <div>
    <app-header text="memory-game" />
    <Nuxt />
  </div>
</template>

<script>
import AppHeader from '../components/AppHeader.vue'
export default {
  name: "DefaultLayout",
  components: {
    AppHeader,
  }
}
</script>

<style scoped>
header {
  font-family: Verdana, "Arial Black",sans-serif;
  background-color: transparent;
  font-size: 0.9em;
  padding-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>