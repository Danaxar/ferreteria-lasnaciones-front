<template>
  <div id="main">
    <ul>
      <li>
        <div>
          <a href="/ventas" class="nav-element">
            <img src="../static/ventas.png" />
            <span>Ventas</span>
          </a>
        </div>
      </li>
      <li>
        <div>
          <a href="/productos" class="nav-element">
            <img src="../static/productos.png" />
            <span>Productos</span>
          </a>
        </div>
      </li>
      <li>
        <div>
          <a href="/inventario" class="nav-element">
            <img src="../static/inventario.png" />
            <span>Inventario</span>
          </a>
        </div>
      </li>
      <li>
        <div>
          <a href="/reportes" class="nav-element">
            <img src="../static/reportes.png" />
            <span>Reportes</span>
          </a>
        </div>
      </li>
      <li>
        <div>
          <a href="/ajustes" class="nav-element">
            <img src="../static/ajustes.png" />
            <span>Ajustes</span>
          </a>
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
  background-color: #4c5f7a;
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
}
</style>
