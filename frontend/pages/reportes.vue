<template>
  <div id="main">
    <Navbar />
    <div id="contenido">Reportes</div>
  </div>
</template>
<script>
import Navbar from '~/components/navbar.vue'
export default {
  name: 'ReportesPage',
  components: { Navbar },
}
</script>
<style scoped>
#main {
  display: flex;
}
</style>
