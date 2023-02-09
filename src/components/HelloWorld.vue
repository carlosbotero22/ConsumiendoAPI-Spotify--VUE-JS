*****************************
****** CARLOS BOTERO ********
*****************************
<template>
  <div>
    <img class="fondo"
      src="https://img.freepik.com/psd-premium/promocion-pagina-negocios-icono-spotify-render-3d-plantilla-banner-instagram-redes-sociales_407398-178.jpg?w=2000">
    <h2 class="m-4">Lo más recientes lanzamientos</h2>
  </div>
  
  <div v-for="value in result" :key="value.id">
     {{ value.name }}
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    result: []
  }),
  created() {
    const config = {
      method: 'get',
      url: 'https://api.spotify.com/v1/browse/new-releases',
      headers: {
        'Authorization': 'Bearer BQCBMcrW_IqeYmDiFXloClhnE5hIO7uhuSS4pWsjBIX1Uty9iMpnMC8PHve3L9B4-pu1qq2MwiB40RNAPMQN_xcQvls4BZp7aWcltFaXeDm5HizcpnOy'
      }
    };
    axios(config)
      .then(function (response) {
        console.log(response)
        this.result = response.data.albums.items
      })
      .catch(function (error) {
        console.log(error);
      });
  },
};
</script>


<style>
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

.fondo {
  width: 100%;
  height: 100%;
}
</style>
