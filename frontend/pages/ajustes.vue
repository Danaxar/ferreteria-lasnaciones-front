<template>
  <div id="main">
    <Navbar />
    <div id="contenido">Ajustes</div>
  </div>
</template>
<script>
import Navbar from '~/components/navbar.vue'
export default {
  name: 'AjustesPage',
  components: { Navbar },
}
</script>
<style scoped>
#main {
  display: flex;
}
</style>
