<template>
  <div>
    <cabecera></cabecera>
    <b-container class="mt-5">
      <b-card v-for="item in items" :key="item['.key']">
        <b-card-text><h3>{{item.nombre}}</h3></b-card-text>
        <b-card-text>{{item.subtitulo}}</b-card-text>
        <b-card-text>{{item.descripcion}}</b-card-text>
        <router-link :to="'/editar/' + item['.key']">Editar</router-link>
        <a href="#" @click="eliminar(item)">Eliminar</a>
      </b-card>
    </b-container>
  </div>
</template>
<script>
import cabecera from './Cabecera'
import sesion from '../mixins/sesion.js'
import firebase from 'firebase'

var post = firebase.database().ref('post');

export default {
  name: 'inicio',
  data(){
  	return{
  		items:[]
  	}
  },
  methods:{
   eliminar(item){
   	var x = confirm('Elimiar registro...????')
   	if(x){
      post.child(item['.key']).remove()
   	}
   }
  },
  components: {
    cabecera
  },
  firebase:{
     items:post
  },
  mixins: [sesion]
}

</script>
