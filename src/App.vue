<template>
  <div id="app">
    <game />
  </div>
</template>

<script>
import Game from "@/components/Game";
export default {
  name: 'App',
  components: {
    Game
  }
}
</script>

<style>

html, body {
  height: 100vh;
}
body {
  margin: 0;
}
</style>