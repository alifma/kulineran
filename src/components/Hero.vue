<template>
    <div class="hero">
        <!-- Desktop -->
        <div class="d-none d-md-block">
            <div class="row mt-4">
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicious Food Menu,</strong>
                                <br> in your gadget</h2>
                            <p>Ayo segera pilih dan pesan makanan favorit anda!</p>
                            <router-link to="/foods" class="btn btn-lg btn-success">
                                <b-icon-arrow-right></b-icon-arrow-right> Pesan
                            </router-link>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <img src="../assets/img/hero.png" width="100%" alt="Test">
                </div>
            </div>
        </div>
        <!-- Mobile -->
        <div class="d-sm-block d-md-none">
            <div class="row mt-4">
                <div class="col-md-6 mb-2">
                    <img src="../assets/img/hero.png" width="100%" alt="Test">
                </div>
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicious Food Menu,</strong>
                                <br> in your gadget</h2>
                            <p>Ayo segera pilih dan pesan makanan favorit anda!</p>
                            <router-link to="/foods" class="btn btn-lg btn-success">
                                <b-icon-arrow-right></b-icon-arrow-right> Pesan
                            </router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>


    </div>

</template>

<script>
    export default {
        name: 'Hero'
    }
</script>

<style>

</style>