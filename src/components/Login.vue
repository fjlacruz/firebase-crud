<template>
<div>
    <b-container class="mt-5">
        <b-row>
            <b-col sm="3">&nbsp;</b-col>
            <b-col sm="6">
                <form @submit.prevent="login">
                    <h3>Login</h3>
                    <b-form-input type="email" placeholder="Email" v-model="email"></b-form-input><br>
                    <b-form-input type="password" placeholder="Contraseña" v-model="contrasena"></b-form-input>
                    <br>
                    <b-button type="submit" variant="outline-primary">Entrar</b-button>
                    <b-button  @click="registro" variant="outline-success">Registrarse</b-button>
                </form>
                <div v-show="mensaje" align="center">
                    <img src="https://127.0.0.1/casa_cambio/application/recursos/imagenes/loader1.gif">
                    Logueando...!!!
                </div>
            </b-col>
            <b-col>&nbsp;</b-col>
        </b-row>
    </b-container>
</div>
</template>

<script>
import firebase from 'firebase'

// Your web app's Firebase configuration
var firebaseConfig = {
    apiKey: "AIzaSyBzU0Xx2-xPeTNPZpz5IsBT4FuWbRHLBFo",
    authDomain: "fir-crud-a081b.firebaseapp.com",
    databaseURL: "https://fir-crud-a081b.firebaseio.com",
    projectId: "fir-crud-a081b",
    storageBucket: "fir-crud-a081b.appspot.com",
    messagingSenderId: "975198073592",
    appId: "1:975198073592:web:9c469feb945c5c5a8d010d",
    measurementId: "G-NEHE5677SB"
};
// Initialize Firebase
firebase.initializeApp(firebaseConfig);
firebase.analytics();

export default {
    name: 'login',
    data() {
        return {
            email: '',
            contrasena: '',
            mensaje: false
        }
    },
    methods: {
        login() {
            if (this.email == '' || this.contrasena=='') {
                alert('debe ingresar su email')
                this.mensaje = false
            } else {
                this.mensaje = true
                firebase.auth().signInWithEmailAndPassword(this.email, this.contrasena)
                    .then((user) => this.$router.push('/inicio'), (error) => alert('Error al loguearse'))
            }

        },
        registro() {
            this.mensaje = true
            firebase.auth().createUserWithEmailAndPassword(this.email, this.contrasena)
                .then((user) => this.$router.push('/inicio')), (error) => alert('Error al registrarse')
        }
    },
    created() {
        firebase.auth().onAuthStateChanged((user) => {
            if (user) {
                this.$router.push('/inicio')
            }
        })
    }
}
</script>
