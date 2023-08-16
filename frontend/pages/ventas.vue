<template>
  <div id="main">
    <Navbar />
    <div id="contenido">
      <!-- Botones superiores -->
      <div class="flex space-around">
        <span>
          <button @click="buscarProductoButton">⌨️</button>
          <input type="text" placeholder="Buscar producto" />
        </span>
        <button class="button-yellow">Producto común</button>
        <button class="button-yellow">Cotizar</button>
        <button class="button-yellow">Ventas del día</button>
        <button class="button-yellow">Factura</button>
      </div>

      <!-- Contenido -->
      <div class="flex">
        <!-- Tabla de productos -->
        <div id="ticket-info">
          <span>
            <h1 style="background-color: yellow; width: 200px">Ticker X</h1>
          </span>
          <table>
            <thead>
              <tr>
                <th>Código</th>
                <th>Producto</th>
                <th>Precio</th>
                <th>Cantidad</th>
                <th>Importe</th>
                <th>Existencias</th>
              </tr>
            </thead>
          </table>
        </div>
        <!-- Vista previa -->
        <div></div>
      </div>

      <!-- Vista buscar teclado (encima de todo) -->
      <div v-show="buscarProducto" id="buscarProductoView">
        <div id="buscarproducto-content">
          <div>
            <h1>Búsqueda de productos</h1>
          </div>
          <div><input type="text" /></div>
          <div>
            <table>
              <thead>
                <tr>
                  <th>Descripción del producto</th>
                  <th>Precio</th>
                  <th>Departamento</th>
                  <th>Inventario</th>
                </tr>
              </thead>
            </table>
          </div>
          <div>
            <button @click="buscarProductoButton">Aceptar</button>
            <button @click="buscarProductoButton">Cancelar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from '~/components/navbar.vue'
export default {
  name: 'VentasPage',
  components: { Navbar },
  data() {
    return {
      buscarProducto: false,
    }
  },
  methods: {
    buscarProductoButton() {
      this.buscarProducto = !this.buscarProducto
    },
  },
}
</script>
<style scoped>
#main {
  display: flex;
}

#contenido {
  background-color: #121212;
  width: 90vw;
}

#ticket-info {
  background-color: #003657;
  border-radius: 30px 30px;
  height: 85vh;
}

#buscarProductoView {
  color: white;
  background-color: rgba(0, 6, 6, 0.5);
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
}

#buscarproducto-content {
  background-color: #ffd700;
  color: black;
  width: 80vw;
  height: 80vh;
  margin: auto;
  border-radius: 30px 30px;
}

.button-yellow {
  color: black;
  background-color: yellow;
  height: 3em;
  border-radius: 30px 30px;
  font-size: 35px;
}

.flex {
  display: flex;
}

.space-around {
  justify-content: space-around;
}
</style>
