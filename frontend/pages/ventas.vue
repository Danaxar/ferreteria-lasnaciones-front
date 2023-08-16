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
          <!-- Título -->
          <div>
            <h1>Búsqueda de productos</h1>
          </div>
          <!-- Filtro -->
          <div>
            <input
              type="text"
              v-model="filtroProducto"
              @change="filtrarProductos"
            />
          </div>
          <!-- Tabla -->
          <div class="center-element">
            <table>
              <thead>
                <tr>
                  <th>Descripción del producto</th>
                  <th>Precio</th>
                  <th>Departamento</th>
                  <th>Inventario</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="producto in listasProductosFiltrados"
                  :key="producto.id"
                  class="fila-producto"
                >
                  <td @click="helloworld" class="celda-producto">
                    {{ producto.producto }}
                  </td>
                  <td @click="helloworld" class="celda-producto">
                    {{ producto.pventa }}
                  </td>
                  <td @click="helloworld" class="celda-producto">
                    {{
                      producto.idDepartamento === null
                        ? '  Sin departamento  '
                        : producto.idDepartamento
                    }}
                  </td>
                  <td @click="helloworld" class="celda-producto">
                    {{ producto.existencia }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
          <!-- Botones -->
          <div id="botones-filtro">
            <button @click="buscarProductoButton" class="btn btn-success">
              Aceptar
            </button>
            <button @click="buscarProductoButton" class="btn btn-danger">
              Cancelar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import Navbar from '~/components/navbar.vue'
export default {
  name: 'VentasPage',
  components: { Navbar },
  data() {
    return {
      buscarProducto: false,
      listaProductos: [],
      listasProductosFiltrados: [],
      productoSeleccionado: null,
      filtroProducto: '',
    }
  },
  methods: {
    buscarProductoButton() {
      this.buscarProducto = !this.buscarProducto
    },
    async pedirListaProductos() {
      const respuesta = await axios.get('http://localhost:8080/api/inventarios')
      console.log('Lista de productos: ', respuesta.data)
      this.listaProductos = respuesta.data
    },
    filtrarProductos() {
      if (this.filtroProducto === '') {
        this.listasProductosFiltrados = []
        return
      }
      this.listasProductosFiltrados = this.listaProductos.filter((producto) =>
        producto.producto.toLowerCase().includes(this.filtroProducto)
      )
    },
    helloworld() {
      console.log('hola mundo')
    },
  },
  mounted() {
    this.pedirListaProductos()
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
  display: flex;
  justify-content: center;
  align-items: center;
}

#buscarproducto-content {
  background-color: #ffd700;
  color: black;
  width: 80vw;
  height: 80vh;
  border-radius: 30px 30px;
  overflow-y: auto;
}

#buscarproducto-content div {
  margin: 1em;
}

#buscarproducto-content h1 {
  text-align: center;
}

#buscarproducto-content input[type='text'] {
  width: 100%;
  height: 2.6em;
  font-size: 35px;
}

#buscarproducto-content table,
th,
td,
tr {
  border: 1px solid black;
}

#buscarproducto-content table {
  width: 100%;
  border-collapse: collapse;
}

#botones-filtro {
  display: flex;
  justify-content: space-around;
}

#botones-filtro button {
  width: 20%;
  height: 3em;
  border-radius: 30px 30px;
  font-size: 25px;
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

.center-element {
  display: flex;
  justify-content: center;
  align-items: center;
}

.space-around {
  justify-content: space-around;
}

.fila-producto:hover {
  background-color: #47432c;
}
</style>
