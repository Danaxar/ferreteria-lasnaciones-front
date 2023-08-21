<template>
  <section class="vh-100 gradient-custom">
    <div class="container py-5 h-100">
      <h1 class="text-white text-center">
        Punto de venta - Ferretería las naciones
      </h1>
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card bg-dark text-white" style="border-radius: 1rem">
            <div class="card-body p-5 text-center">
              <div class="mb-md-5 mt-md-4 pb-5">
                <h2 class="fw-bold mb-2 text-uppercase">Iniciar sesión</h2>
                <p class="text-white-50 mb-5">
                  Por favor ingresa tu nombre de usuario y contraseña
                </p>

                <div class="form-outline form-white mb-4">
                  <select
                    v-model="username"
                    class="form-select custom-select"
                    id="region"
                  >
                    <option value="" disabled selected hidden>
                      Selecciona una opción
                    </option>
                    <option
                      v-for="(objeto, indice) in listaUsuarios"
                      :key="indice"
                    >
                      {{ objeto.nombre_usuario }}
                    </option>
                  </select>
                  <label class="form-label" for="typeUsernameX"
                    >Nombre de usuario</label
                  >
                </div>

                <div class="form-outline form-white mb-4">
                  <input
                    v-model="password"
                    type="password"
                    id="typePasswordX"
                    class="form-control form-control-lg"
                  />
                  <label class="form-label" for="typePasswordX"
                    >Contraseña</label
                  >
                </div>
                <button
                  class="btn btn-outline-light btn-lg px-5"
                  type="submit"
                  @click="login"
                >
                  Login
                </button>

                <div
                  class="d-flex justify-content-center text-center mt-4 pt-1"
                >
                  <a href="#!" class="text-white"
                    ><i class="fab fa-facebook-f fa-lg"></i
                  ></a>
                  <a href="#!" class="text-white"
                    ><i class="fab fa-twitter fa-lg mx-4 px-2"></i
                  ></a>
                  <a href="#!" class="text-white"
                    ><i class="fab fa-google fa-lg"></i
                  ></a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',
  data() {
    return {
      username: '',
      password: '',

      // Lista de usuarios
      listaUsuarios: null,
    }
  },
  methods: {
    async getAllUsuarios() {
      const respuesta = await axios.get('http://localhost:8080/api/usuarios')
      this.listaUsuarios = respuesta.data
      console.log(respuesta.data)
    },
    async login() {
      const usuario = {
        nombre_usuario: this.username,
        contrasena_usuario: this.password,
      }

      const respuesta = await axios.post(
        'http://localhost:8080/api/usuarios/login',
        usuario
      )

      console.log(respuesta.data)

      if (respuesta.data === true) {
        window.location.href = '/ventas'
      }
    },
  },
  mounted() {
    this.getAllUsuarios()
  },
}
</script>

<style scoped>
.gradient-custom {
  /* fallback for old browsers */
  background: #6a11cb;

  /* Chrome 10-25, Safari 5.1-6 */
  background: -webkit-linear-gradient(
    to right,
    rgba(106, 17, 203, 1),
    rgba(37, 117, 252, 1)
  );

  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background: linear-gradient(
    to right,
    rgba(106, 17, 203, 1),
    rgba(37, 117, 252, 1)
  );
}
</style>
