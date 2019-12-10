<template>
  <div>
    <cabecera></cabecera>
    <b-container class="mt-5">
      <h3>Editar Post</h3>
      <form @submit.prevent="editarPost">
        <div>
          <b-form-input type="text" placeholder="Nombre del post" v-model="editarItem.nombre"></b-form-input><br>
          <b-form-input type="text" placeholder="Subtitulo" v-model="editarItem.subtitulo"></b-form-input><br>
          <b-form-input type="text" placeholder="descripcion" v-model="editarItem.descripcion"></b-form-input>
          <br>
          <b-button type="submit" variant="outline-primary">Editar</b-button>
        </div>
      </form>
      <div v-show="mensaje" align="center">
        <img src="https://127.0.0.1/casa_cambio/application/recursos/imagenes/loader1.gif">
        Editando...!!!
      </div>
    </b-container>
  </div>
</template>
<script>
import cabecera from './Cabecera'
import firebase from 'firebase'
import sesion from '../mixins/sesion.js'

var post = firebase.database().ref('post');

export default {
  name: 'editar',

  data() {
    return {
      editarItem: {},
      items: {},
      mensaje: false
    }
  },
  methods: {

    editarPost() {
    	this.mensaje = true
      post.child(this.$route.params.id).update(this.editarItem)
      this.$router.push('/inicio')
    }
  },
  firebase: {
    items: post

  },
  created() {
    //let item = this.itemsObj[this.$route.params.id]
    firebase.database().ref('post/' + this.$route.params.id).once('value', snapshot => {
      const item = snapshot.val()
      this.editarItem = {
        nombre: item.nombre,
        subtitulo: item.subtitulo,
        descripcion: item.descripcion
      }
    })

  },

  components: {
    cabecera
  },
  mixins: [sesion]
}

</script>
