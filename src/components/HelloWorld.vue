*****************************
****** CARLOS BOTERO ********
*****************************
<template>
  <div class="release">
    <img class="fondo"
      src="https://img.freepik.com/psd-premium/promocion-pagina-negocios-icono-spotify-render-3d-plantilla-banner-instagram-redes-sociales_407398-178.jpg?w=2000">
    <h2 class="m-4">Lo más recientes lanzamientos</h2>

    <li class="info" v-for="item of result" :key="item.id">
      {{ item.name }}
    </li>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      result: [],
    };
  },
  methods: {
    async fetch() {
      const config = {
        method: "get",
        url: "https://api.spotify.com/v1/browse/new-releases",
        headers: {
          Authorization:
            "Bearer BQCBMcrW_IqeYmDiFXloClhnE5hIO7uhuSS4pWsjBIX1Uty9iMpnMC8PHve3L9B4-pu1qq2MwiB40RNAPMQN_xcQvls4BZp7aWcltFaXeDm5HizcpnOy",
        },
      };
      let data = this.result;

      const response = await axios(config)
        .then(function ({
          data: {
            albums: { items },
          },
        }) {
          return items;
        })
        .catch(function (error) {
          console.log(error);
        });
      this.result = response;
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

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
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
