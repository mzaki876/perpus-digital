<template>
    <div class="container-fluid">
        <div class="row py-5 d-flex justify-content-center">
            <div class="col-lg-6">
                <nuxt-link to="/pengunjung/tambah">
                    <div class="card bg-pengunjung rounded-5">
                        <div class="card-body">
                            <h2 class="fw-bold">PENGUNJUNG</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>

            <div class="col-lg-6">
                <nuxt-link to="/buku">
                    <div class="card bg-buku rounded-5">
                        <div class="card-body">
                            <h2 class="fw-bold">BUKU</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
        </div>
    </div>
</template>

<style scoped>
.container-fluid {
    /* padding: 0;
    margin: 0; */
    background-color: #ffffff;
}

.card {
    height: 250px;
    box-shadow: 1px 1px 10px hsl(0, 0%, 100%)
}

.card.bg-pengunjung {
    background-image: url('@/assets/img/hhh.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}

.card.bg-buku {
    background: url('@/assets/img/buku.jpg') no-repeat center center;
    background-size: cover;
}

.pengunjung {
    background-color: #89B6D6;
}

.buku {
    background-color: #89B6D6;
}

h2 {
    color:  rgb(255, 255, 255);
    font-family: "Irish Grover", system-ui;
}

.container-fluid {
    background-image: url("@/assets/img/bgp.jpg");
    background-size:cover;
    height: 100vh;
    padding-top: 160px;
}

</style>

