<template>
  <div id="app">
    <game-field />
  </div>
</template>

<script>
import GameField from '@/components/GameField.vue'

export default {
  name: 'App',
  components: {
    GameField
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
