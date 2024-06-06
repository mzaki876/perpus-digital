<template>
    <div class="wrapper">
    <div class="content"></div>
        <div class="container-fluid">
            <nuxt-link to="/buku/" class="btn btn-dark btn-lg mt-4">KEMBALI</nuxt-link>
                <nuxt-link to="/" class="btn btn-dark btn-lg mt-4 ms-3">SELESAI</nuxt-link>
                    <h2 class="text-center my-4 text-white fw-bold bg-secondary" >RINCIAN BUKU</h2>
            <div class="row d-flex justify-content-center flex-md-wrap" style="padding-top: 50px;">
                <div class="col-3 ">
                    <img :src="buku?.cover"  class="cover row img-fluid" alt="cover buku"   style="width: 250px; padding-top: 100px;">
                    <div class="row">
                    </div>
                </div>
                <div class="col-8">
                    <div class="row">
                        <h1 class="text start text-light fw-bold text-center my-4">{{ buku?.judul }}</h1>
                    </div>
                    <div class="row">
                    <div class="badge bg-secondary">{{ buku?.kategori?.nama }}</div>
                        <ul class="list-group list-group-flush">
                            <li class="list-group-item">PENULIS: {{ buku?.penulis }}</li>
                            <li class="list-group-item">PENERBIT: {{ buku?.penerbit }}</li>
                            <li class="list-group-item">TAHUN TERBIT: {{ buku?.tahun_terbit }}</li>
                            <li class="list-group-item">RAK: {{ buku?.rak }}</li>
                            <li class="list-group-item">KATEGORI: {{ buku?.kategori?.nama }}</li>
                            <li class="list-group-item">DESKRIPSI: {{ buku?.deskripsi }}</li>
                        </ul>                       
                    </div>
                </div>
            </div>
        </div>
        </div>
</template>
<script setup>
//   import { onMounted } from 'vue';

const supabase = useSupabaseClient()
const route = useRoute()
const buku = ref()

const getBookByid = async () => {
    const { data, error } = await supabase
    .from('buku')
    .select(`*, kategori(*)`)
    .eq('id', route.params.id)
    .maybeSingle()
    if(data) buku.value = data

}

onMounted(() => {
    getBookByid()
})

</script>
<style scoped>
.content {
    background-image: url("@/assets/img/buku.jpg");
    height: 100vh;
    font-family: "";
    background-size: cover;
    background-repeat: no-repeat;
    /* font-family: "Jockey One"; */
    position: fixed;
    top: 0;
    /* background-position: cent; */
    bottom: 0;
    left: 0;
    right: 0;
    z-index: -1;
}
.container-fluid {
    padding-top: 160px;
}
</style> 