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
      <div class="flex" style="justify-content: space-around;">
        <!-- Tabla de productos -->
        <div id="ticket-info">
          <span>
            <h1 style="background-color: yellow; width: 200px">Ticket X</h1>
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
            <tbody>
              <tr v-for="producto in carrito" :key="producto.codigoProducto">
                <td>{{ producto.codigoProducto }}</td>
                <td>{{ producto.producto }}</td>
                <td>{{ producto.pventa }}</td>
                <td><input type="number" v-bind:value="producto.cantidad" @change="updateCantidadProducto(producto)" /></td>
                <td>{{ producto.pventa }}</td>
                <td>{{ producto.existencia }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <!-- Vista previa del ticket-->
        <div>
          <div id="ticket-preview">
            <img src="../static/logo.png" alt="logo" width="250px"/>
            <p>
              LAS NACIONES 2453
              <br />
              ferreterialasnaciones@gmail.com
            </p>
            <div>
              <table>
                <thead>
                  <tr>
                    <th>Cant.</th>
                    <th>Descripción</th>
                    <th>Importe</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="producto in ticket" :key="producto.codigoProducto">
                    <td>{{ producto.cantidad }}</td>
                    <td>{{ producto.producto }}</td>
                    <td>{{ producto.pventa }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          <div>
            <button class="button-yellow" @click="cobrar">
              COBRAR
            </button>
          </div>
        </div>
      </div>

      <!-- Vista buscar teclado (encima de todo) -->
      <div v-show="buscarProducto" id="buscarProductoView">
        <div id="buscarproducto-content">
          <!-- Título -->
          <div >
            <div style="display: flex; justify-content: right;">
              <button class="btn btn-danger" @click="buscarProductoButton">
               X
              </button>
            </div>
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
          <div class="div-table-center">
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
                  <td @click="addCarrito(producto)" class="celda-producto">
                    {{ producto.producto }}
                  </td>
                  <td @click="addCarrito(producto)" class="celda-producto">
                    {{ producto.pventa }}
                  </td>
                  <td @click="addCarrito(producto)" class="celda-producto">
                    {{
                      producto.idDepartamento === null
                        ? '  Sin departamento  '
                        : producto.idDepartamento
                    }}
                  </td>
                  <td @click="addCarrito(producto)" class="celda-producto">
                    {{ producto.existencia }}
                  </td>
                </tr>
              </tbody>
            </table>
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
      listaProductos: [], // 3000 productos
      listasProductosFiltrados: [],
      productoSeleccionado: null,
      filtroProducto: '',
      carrito: [],
      ticket: []
    }
  },
  methods: {
    buscarProductoButton() {
      this.buscarProducto = !this.buscarProducto
      this.filtroProducto = ''
      this.listasProductosFiltrados = []
    },
    async pedirListaProductos() {
      const respuesta = await axios.get('http://localhost:8080/api/inventarios')
      this.listaProductos = respuesta.data
    },
    filtrarProductos() {
      if (this.filtroProducto === '') {
        this.listasProductosFiltrados = []
        return
      }
      this.listasProductosFiltrados = this.listaProductos.filter(
        (producto) =>
          producto.producto.toLowerCase().includes(this.filtroProducto) ||
          producto.producto.includes(this.filtroProducto)
      )
    },
    addCarrito(producto) {
      producto.cantidad = 1;
      this.carrito.push(producto)
      this.ticket = JSON.parse(JSON.stringify(this.carrito))
      this.buscarProducto = false
      this.filtroProducto = ''
      this.listasProductosFiltrados = []
      console.log(this.carrito)
    },
    cobrar(){
      console.log(this.carrito);
    },
    updateCantidadProducto(producto){
      producto.cantidad++;
      this.ticket = JSON.parse(JSON.stringify(this.carrito))
      console.log(producto.cantidad);
    },
    printProdcut(producto){
      console.log(producto);
    }
  },
  mounted() {
    this.pedirListaProductos()
  },
  updated() {
    
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
  width: 60vw;
}

#ticket-info table {
  width: 100%;
  border-collapse: collapse;
  color: white;
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
  /* overflow-y: auto; */
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
  font-size: 30px;
}

.div-table-center {
  height: 50vh;
  overflow-y: auto;
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

#ticket-preview{
  color:white;
  background-color: #474040;
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

.div-table-center {
  display: flex;
  justify-content: center;
  /* align-items: center; */
}

.space-around {
  justify-content: space-around;
}

.fila-producto:hover {
  background-color: white;
  color: black;
}
</style>
