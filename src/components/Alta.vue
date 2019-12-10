<template>
  <div>
    <cabecera></cabecera>
    <b-container class="mt-5">
      <h3>Alta post</h3>
      <form @submit.prevent="guardarpost">
        <div>
          <b-form-input type="text" placeholder="Nombre del post" v-model="nombre"></b-form-input><br>
          <b-form-input type="text" placeholder="Subtitulo" v-model="subtitulo"></b-form-input><br>
          <b-form-input type="text" placeholder="descripcion" v-model="descripcion"></b-form-input>
          <br>
          <b-button type="submit" variant="outline-primary">Registrar</b-button>
        </div>
      </form>
    </b-container>
  </div>
</template>



<script>
import cabecera from './Cabecera'
import firebase from 'firebase'
import sesion from '../mixins/sesion.js'

var post = firebase.database().ref('post');

export default {
  name: 'alta',

  data() {
        return {
            nombre: '',
            subtitulo: '',
            descripcion: ''
        }
    },
    methods:{

    	guardarpost(){
    		post.push({nombre:this.nombre,subtitulo:this.subtitulo,descripcion:this.descripcion})
    		this.nombre = ''
    		this.subtitulo =''
    		this.descripcion =''
    	}
    },

  components: {
    cabecera
  },
  mixins: [sesion]
}

</script>
