<template>
    <div class="wrapper">
        <div class="content"></div>
    <div class="container-fluid">
        <div class="row">
        <div class="col-lg-12">
            <nuxt-link to="/pengunjung">
            <button type="button" class="btn btn-outline-dark mt-4 btn-lg">KEMBALI</button></nuxt-link>
            <nuxt-link to="/">
                <button type="button" class="btn btn-outline-dark btn-lg mt-4 ms-3">SELESAI</button></nuxt-link>
            <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
            <div class="my-3">
            <form @submit.prevent="getPengunjung">
                <input v-model="keyword" type="search" class="form-control form-control-lg rounded-5" placeholder="Cari..." @input= "getPengunjung"/>
            </form>
            </div>
            <div class="my-3">menampilkan {{ visitors.length }}</div>
            <div class="table-responsive">
            <table class="table table-bordered border-dark">
            <thead>
                <tr class="text-center">
                <td>ID</td>
                <td>TANGGAL</td>
                <TD>WAKTU</TD>
                <td>NAMA</td>
                <td>KEANGGOTAAN</td>
                <td>KELAS</td>
                <td>KEPERLUAN</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(visitors,i) in visitors" :key="i" class="text-center">
                <td>{{ i+1 }}.</td>
                <td>{{ visitors.tanggal }}</td> 
                <td>{{ visitors.waktu}} </td>
                <td>{{ visitors.nama }}</td>
                <td>{{ visitors.keanggotaan.nama }}</td>
                <td>{{ visitors.tingkat}}-{{ visitors.jurusan }}{{ visitors.kelas }}</td>
                <td>{{ visitors.keperluan.nama }}</td>
                
                
                </tr>
            </tbody>
            </table>
            </div>
        </div>
        </div>
    </div>
    </div>
</template>
<script setup>
const supabase= useSupabaseClient()

const keyword= ref('')
const visitors = ref([])
const getPengunjung =async () => {
    const { data, error } = await supabase
    .from('pengunjung')
    .select(`*, keanggotaan(*), keperluan(*)`)
    .ilike("nama", `%${keyword.value}%`)
    if(data) visitors.value = data
}
onMounted(() =>{
    getPengunjung()
})



</script>
<style scoped>
.content{
    background-image: url('@/assets/img/BGG.jpeg');
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
.h2{
    color:white;
}

.wrapper{
    padding-top: 160px;
}
</style>