<template>
  <div id="main">
    <Navbar />
    <div id="contenido">Productos</div>
  </div>
</template>
<script>
import Navbar from '~/components/navbar.vue'
export default {
  name: 'ProductosPage',
  components: { Navbar },
}
</script>
<style scoped>
#main {
  display: flex;
}
</style>
