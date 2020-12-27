<template>
  <!-- Old Navbar -->
  <!-- <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container">
      <a class="navbar-brand" href="#">Kulineran</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/cart">Keranjang
              <b-icon-bag></b-icon-bag><span
                class="badge badge-success ml-2">{{updateCart ? updateCart.length : jumlah_pesanan.length}}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav> -->

  <div class="container px-0">
    <b-navbar toggleable="lg" type="light">
      <b-navbar-brand href="#">Kulineran</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <router-link class="nav-link" to="/cart">Keranjang
            <b-icon-bag></b-icon-bag><span
              class="badge badge-success ml-2">{{updateCart ? updateCart.length : jumlah_pesanan.length}}</span>
          </router-link>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'Navbar',
    data() {
      return {
        jumlah_pesanan: []
      }
    },
    props: ['updateCart'],
    methods: {
      setJumlah(data) {
        this.jumlah_pesanan = data
      }
    },
    mounted() {
      axios.get('http://localhost:3000/keranjangs/')
        .then(response =>
          // handle success
          this.setJumlah(response.data),
        )
        .catch(error =>
          // handle error
          console.log("Gagal : ", error)
        )
    }
  }
</script>

<style>

</style>