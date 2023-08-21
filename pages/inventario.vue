<template>
  <div id="main">
    <Navbar />
    <div id="contenido">Inventario</div>
  </div>
</template>
<script>
import Navbar from '~/components/navbar.vue'
export default {
  name: 'InventarioPage',
  components: { Navbar },
}
</script>
<style scoped>
#main {
  display: flex;
}
</style>
