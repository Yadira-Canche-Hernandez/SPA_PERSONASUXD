<script>
import axios from 'axios'



export default {

  data() {
    return {
      
    }
  },

  mounted() {
    axios.get(API_URL)
      .then((response) => {
        //paginas
        this.info = response.data.info;
        //resultados
        this.personajes = response.data.results;
      })
  },

  methods: {
    
    //informacion de un personaje
    Registro( ) {  
      axios
        .post("/api/guardarPersonasUxd.php", {
        nombre: this.nombre,
        objetivos:this.objetivos,
        frustraciones: this.frustraciones,
        motivaciones: this.motivaciones,
        marcas: this.marcas,
        //completar las variables, estas deben llamarse como las que se recibirán en el backend sin el símbolo del dolar $
        })
        .then((response) => {
        console.log(response.status)
        });
      
    }
  },
}

</script>

<template class="flex mx-auto">

  
</template>