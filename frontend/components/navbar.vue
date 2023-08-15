<template>
  <div id="main">
    <ul>
      <li>
        <div class="nav-element">
          <img src="../static/ventas.png" />
          <a href="/ventas">Ventas</a>
        </div>
      </li>
      <li>
        <div class="nav-element">
          <img src="../static/productos.png" />
          <a href="/productos">Productos</a>
        </div>
      </li>
      <li>
        <div class="nav-element">
          <img src="../static/inventario.png" />
          <a href="/inventario">Inventario</a>
        </div>
      </li>
      <li>
        <div class="nav-element">
          <img src="../static/reportes.png" />
          <a href="/reportes">Reportes</a>
        </div>
      </li>
      <li>
        <div class="nav-element">
          <img src="../static/ajustes.png" />
          <a href="/ajustes">Ajustes</a>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'Navbar',
}
</script>
<style scooped>
#main {
  width: 10vw;
  background-color: #4c5f7a;
  /* color: white; */
  height: 100vh;
}

#main ul li {
  transition: 0.2s; /* Regresa a la normalidad */
}

#main ul li:hover {
  transform: scale(1.1);
  transition: 0.2s; /* Se agranda */
}

/* Tamaño de la imagen */
#main ul li img {
  width: 100px;
  height: 100px;
}

/* Configurar estilo del enlace */
#main ul li a {
  color: white;
  text-decoration: none;
  font-size: 20px;
}

#main ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 100vh; /* Esto establece la altura de la lista al 100% del alto de la ventana */
  list-style: none; /* Quita los marcadores de lista predeterminados */
}

.nav-element {
  width: 10vw;
  display: flex;
  flex-direction: column;
  /* background-color: aquamarine; */
}
</style>
