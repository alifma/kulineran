<template>
    <div class="car">
        <Navbar :updateCart="cart" />
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
                            <li class="breadcrumb-item active" aria-current="page">Cart</li>
                        </ol>
                    </nav>
                </div>
            </div>
            <div class="row">
                <div class="col">
                    <h2>Keranjang <strong>Saya</strong></h2>
                    <div class="table-responsive mt-3">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th align="center" scope="col">#</th>
                                    <th scope="col">Foto</th>
                                    <th scope="col">Makanan</th>
                                    <th align="center" scope="col">Keterangan</th>
                                    <th align="center" scope="col">Jumlah</th>
                                    <th align="center" scope="col">Harga</th>
                                    <th align="center" scope="col">Total Harga</th>
                                    <th align="center" scope="col">Hapus</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(cart, index) in cart" :key="cart.id">
                                    <th>{{index+1}}</th>
                                    <td><img :src="'/img/'+cart.product.gambar" class="img-fluid shadow" width="250"
                                            alt=""></td>
                                    <td>{{cart.product.nama}}</td>
                                    <td>{{cart.keterangan ? cart.keterangan:"-"}}</td>
                                    <td align="center">{{cart.jumlah_pemesanan}}</td>
                                    <td align="right">Rp. {{cart.product.harga}}</td>
                                    <td align="right"><strong>Rp.
                                            {{cart.jumlah_pemesanan * cart.product.harga}}</strong></td>
                                    <td align="center" class="text-danger">
                                        <b-icon-trash @click="deleteCart(cart.id)"></b-icon-trash>
                                    </td>
                                </tr>
                                <tr>
                                    <td colspan="6" align="right">
                                        <strong>Total Harga :</strong>
                                    </td>
                                    <td align="right">
                                        <strong>Rp. {{totalHarga}}</strong>
                                    </td>
                                    <td></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Form Checkout -->
            <div class="row justify-content-end">
                <div class="col-md-4">
                    <form v-on:submit.prevent>
                        <div class="form-group mt-4">
                            <label for="nama">Nama :</label>
                            <input type="text" class="form-control" v-model="pesan.nama">
                        </div>
                        <div class="form-group mt-4">
                            <label for="noMeja">Nomor Meja :</label>
                            <input type="text" class="form-control" v-model="pesan.noMeja">
                        </div>
                        <button type="submit" class="btn float-right btn-success" @click="checkout">
                            <b-icon-cart class="mr-2"></b-icon-cart> Pesan
                        </button>
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
        name: 'Cart',
        components: {
            Navbar
        },
        data() {
            return {
                cart: [],
                pesan: {}
            }
        },
        methods: {
            setCart(data) {
                this.cart = data
            },
            deleteCart(id) {
                axios.delete('http://localhost:3000/keranjangs/' + id)
                    .then(() => {
                        this.$toast.error('Items dihapus dari keranjang', {
                            type: 'error',
                            position: 'top-right',
                            duration: 3000,
                            dismissable: true
                        })
                        // Reload Axios
                        // Make a request for a user with a given ID
                        axios.get('http://localhost:3000/keranjangs')
                            .then(response =>
                                // handle success
                                this.setCart(response.data)
                            )
                            .catch(error =>
                                // handle error
                                console.log("Gagal : ", error)
                            )
                    })
                    .catch(error =>
                        // handle error
                        console.log("Gagal : ", error)
                    )
            },
            checkout() {
                // console.log("Pesan ", this.pesan)
                if (this.pesan.nama && this.pesan.noMeja) {
                    this.pesan.cart = this.cart;

                    axios.post("http://localhost:3000/pesanans", this.pesan)
                        .then(() => {
                            // Hapus keranjang
                            this.cart.map((item) => {
                                return axios.delete('http://localhost:3000/keranjangs/' + item.id)
                            })
                            this.$router.push({
                                path: "/success"
                            })
                            this.$toast.success('Pemesanan Berhasil', {
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
                    this.$toast.error('Nama dan Nomor Meja tidak boleh kosong', {
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
            axios.get('http://localhost:3000/keranjangs')
                .then(response =>
                    // handle success
                    this.setCart(response.data)
                )
                .catch(error =>
                    // handle error
                    console.log("Gagal : ", error)
                )
        },
        computed: {
            totalHarga() {
                return this.cart.reduce(function (items, data) {
                    return items + (data.product.harga * data.jumlah_pemesanan)
                }, 0)
            }
        }
    }
</script>

<style>

</style>