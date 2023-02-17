*****************************
****** CARLOS BOTERO ********
*****************************


<template><!-- barra de navegacion -->
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <h4 class="navbar-nav me-auto mb-2 mb-lg-0">SPO<span style="color: green;">TIFY</span></h4>
      <div class="d-flex align-items-center">

        <input v-model="buscar" class="form-control mr-sm-2 m-1" type="search" placeholder="Buscar" aria-label="Search"
          v-on:keyup.enter="mostrarDatos">

        <button class="btn btn-outline-success my-2 my-sm-0" type="submit" v-on:click="mostrarDatos">Buscar</button>
        <a class="text-reset me-3" href="#">
          <i class="fas fa-shopping-cart"></i>
        </a>
        <div class="dropdown">
          <a class="dropdown-toggle d-flex align-items-center hidden-arrow" href="#" id="navbarDropdownMenuAvatar"
            role="button" data-mdb-toggle="dropdown" aria-expanded="false">
            <img src="https://mdbcdn.b-cdn.net/img/new/avatars/2.webp" class="rounded-circle" height="25"
              alt="Black and White Portrait of a Man" loading="lazy" />
          </a>
        </div>
      </div>
    </div>
  </nav>

  <!-- banner de fondo -->
  <img class="fondo"
    src="https://img.freepik.com/psd-premium/promocion-pagina-negocios-icono-spotify-render-3d-plantilla-banner-instagram-redes-sociales_407398-178.jpg?w=2000">

  <!-- cards lanzamientos -->
  <div class="container-fluid">

    <h2 class="m-4">Lo más recientes lanzamientos</h2>

    <div class="row">
      <template class="info" v-for="item of resultTmp" v-bind:key="item.id">
        <div class="card col-sm-3">
          <img class="card-img-top"
            src="https://cdn.computerhoy.com/sites/navi.axelspringer.es/public/media/image/2021/04/spotify-2318979.jpg?tf=3840x"
            alt="Card image cap">
          <div class="card-body">
            <h5 class="card-title">{{ item.name }}</h5>
            <p class="card-text-dark">With supporting text below as a natural lead-in to additional content.</p>
            <a href="https://open.spotify.com/collection/tracks" class="btn btn-primary">Reproducir</a>
          </div>
        </div>
      </template>   
    </div>
  </div>
  
</template>



<script>
// consumiendo API REST y filtrando información
import axios from "axios";

export default {

  data() {
    return {
      result: [],
      resultTmp: [],
      buscar: '',
    };
  },
  methods: {
    mostrarDatos: function () {
      this.resultTmp = this.result.filter((item) =>
        item.name.toLowerCase().includes(this.buscar.toLowerCase()));
    },
    changeResult: function (result) {
      this.result = result;
      this.resultTmp = result;
    },
    async fetch() {
      const config = {
        name: this.name,
        method: "get",
        url: "https://api.spotify.com/v1/browse/new-releases",
        headers: { Authorization: "Bearer BQAv6eM_HCsJLCiE2pdoCVSp1nYA4v7vwJvLQmL1TezN7VOp9LwcCrbmNm1pZ_EwdjP8XxEHVqGB7ZWiUmDIXjwziFTGuKeCC55NG4_ZUpEVResKIy-F" }
      };
      try {
        const response = await axios(config);
        this.changeResult(response.data.albums.items);
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    this.fetch();
  },
};
</script>


<style>
h2 {
  color: #42b983;
}

.release {
  background-color: black;
}

.fondo {
  width: 100%;
  height: 100%;
}
</style>