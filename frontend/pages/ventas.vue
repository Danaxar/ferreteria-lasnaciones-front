<template>
  <div id="main">
    <Navbar />
    <div id="contenido">VENTAS</div>
  </div>
</template>
<script>
import Navbar from '~/components/navbar.vue'
export default {
  name: 'VentasPage',
  components: { Navbar },
}
</script>
<style scoped>
#main {
  display: flex;
}
</style>
