<template>
<div>
    <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">Firebase crud</b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
                
                <router-link to="/inicio">
                    <font color="white">Inicio&nbsp;</font>
                </router-link>
            </b-navbar-nav>
            <b-navbar-nav>
                <router-link to="/alta">
                    <font color="white">&nbsp;Alta Post</font>
                </router-link>
            </b-navbar-nav>
            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <b-nav-item href="#" @click="salir">Salir</b-nav-item>
            </b-navbar-nav>
        </b-collapse>
    </b-navbar>
</div>
</template>

<script>
import firebase from 'firebase'

export default {
    name: 'cabecera',
    methods: {
        salir() {
            firebase.auth().signOut().then(() => this.$router.push('/'))
        }
    }

}
</script>
