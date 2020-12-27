<template>
    <div>
        <Navbar />
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col text-center">
                    <img src="../assets/img/menunggu.png" width="300" alt="">
                    <h2><strong>Pesanan Sukses</strong></h2>
                    <h4>Pesanan anda sedang diproses <br>selamat menunggu !</h4>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Navbar from '@/components/Navbar.vue'
    export default {
        name: 'Success',
        components: {
            Navbar
        }

    }
</script>

<style>

</style>