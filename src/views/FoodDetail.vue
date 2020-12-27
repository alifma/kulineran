<template>
    <div class="food-detail">
        <Navbar />
        <div class="container">
            <!-- Breadcrumb -->
            <div class="row mt-5">
                <div class="col">
                    <nav aria-label="breadcrumb">
                        <ol class="breadcrumb">
                            <li class="breadcrumb-item">
                                <router-link to="/" class="text-dark ">Home</router-link>
                            </li>
                            <li class="breadcrumb-item">
                                <router-link to="/foods" class="text-dark ">Foods</router-link>
                            </li>
                            <li class="breadcrumb-item active" aria-current="page">Library</li>
                        </ol>
                    </nav>
                </div>
            </div>
            <div class="row mt-4">
                <div class="col-md-6">
                    <img :src="'/img/'+product.gambar" class="img-fluid shadow">
                </div>
                <div class="col-md-6">
                    <h2 class="mt-sm-4 mt-md-0"><strong>{{product.nama}}</strong></h2>
                    <hr>
                    <h4>Harga : <strong>Rp. {{product.harga}}</strong></h4>
                    <form v-on:submit.prevent>
                        <div class="form-group mt-4">
                            <label for="jumlah_pemesanan">Jumlah Pesanan</label>
                            <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan">
                        </div>
                        <div class="form-group">
                            <label for="jumlah_pemesanan">Keterangan</label>
                            <textarea class="form-control mb-4" placeholder="keterangan seperti : Pedas, Nasi setengah"
                                v-model="pesan.keterangan"></textarea>
                            <button type="submit" class="btn btn-success" @click="pemesanan">
                                <b-icon-cart class="mr-2"></b-icon-cart> Pesan
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Navbar from '@/components/Navbar.vue'
    import axios from 'axios'
    export default {
        name: 'FoodDetail',
        components: {
            Navbar
        },
        data() {
            return {
                product: {},
                pesan: {}
            }
        },
        methods: {
            setProduct(data) {
                this.product = data
            },
            pemesanan() {
                if (this.pesan.jumlah_pemesanan) {
                    this.pesan.product = this.product
                    axios.post("http://localhost:3000/keranjangs", this.pesan)
                        .then(() => {
                            this.$toast.success('Berhasil menambahkan ke keranjang', {
                                type: 'success',
                                position: 'top-right',
                                duration: 3000,
                                dismissable: true
                            })
                        })
                        .catch((err) => {
                            console.log("Gagal", err)
                        })
                } else {
                    this.$toast.error('Jumlah barang wajib diisi', {
                        type: 'error',
                        position: 'top-right',
                        duration: 3000,
                        dismissable: true
                    })
                }
            }
        },
        mounted() {
            // Make a request for a user with a given ID
            axios.get('http://localhost:3000/products/' + this.$route.params.id)
                .then(response =>
                    // handle success
                    this.setProduct(response.data)
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