<template>
    <div class="container-fluid">
    <div class="content d-flex justify-content-center">
        <div class="row ">
        <div class="col-lg-11">
            <form @submit.prevent="kirimData">
            <h2 class="text-center my-4 text-light">ISI DATA KUNJUNGAN</h2>
            <div class="mb-3">
                <input v-model="form.nama" type="text" placeholder="Nama ..." class="form-control form-control-lg rounded-5" required>
            </div>
            <div class="mb-3">
                <select v-model="form.keanggotaan" @change="resetkelas" class="form-control form-control-lg form-select rounded-5">
                <option value="" disabled>KEANGGOTAAN</option>
                <option v-for="(keanggotaan,i) in members" :key="i" :value="keanggotaan.id">{{ keanggotaan.nama }}</option>
                </select>
            </div>
            <div class="mb-3" v-if="form.keanggotaan == '1'">
                <div class="row">
                <div class="col-md-4">
                    <select v-model="form.tingkat" class="form-control form-control-lg form-select rounded-5 mb-2">
                    <option value="" disabled>TINGKAT</option>
                    <option value="X">X</option>
                    <option value="XI">XI</option>
                    <option value="XII">XII</option>
                    </select>
                </div>
                <div class="col-md-4">
                <select v-model="form.jurusan" class="form-control form-control-lg form-select rounded-5 mb-2">
                    <option value="" disabled>JURUSAN</option>
                    <option value="PPLG">PPLG</option>
                    <option value="TJKT">TJKT</option>
                    <option value="TSM">TSM</option>
                    <option value="DKV">DKV</option>
                    <option value="TOI">TOI</option>
                    </select>
                </div>
                <div class="col-md-4 ">
                    <select v-model="form.kelas" class="form-control form-control-lg form-select rounded-5 mb-2">
                    <option value="" disabled>KELAS</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    </select>
                </div>
                </div>
            </div>
            <div class="mb-3">
                <select v-model="form.keperluan"  class="form-control form-control-lg form-select rounded-5">
                <option value="" disabled>KEPERLUAN</option>
                <option v-for="(item,i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
                </select>
            </div>
            <input type="submit"  class="btn btn-dark btn-lg rounded-5 " style="width:10rem; margin-left: 80px;" value="Kirim">
            </form>
        </div>
        </div>
    </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const members = ref ([])
const objectives = ref([])
const form = ref({
    nama: "",
    keanggotaan: "",
    tingkat: "",
    jurusan: "",
    kelas: "",
    keperluan: "",
})
const kirimData = async () => {
    const { error } = await supabase.from('pengunjung').insert([form.value])
    if(!error) navigateTo('/pengunjung/')
}
const getKeanggotaan = async () => {
    const { data, error } = await supabase.from('keanggotaan').select('*')
    if(data) members.value = data
}
const getKeperluan = async () => {
    const { data, error } = await supabase.from('keperluan').select('*')
    if(data) objectives.value = data
}

const resetkelas = e => {
    if(e.target.value === '2' || '3' || '4'){
    form.value.tingkat = ''
    form.value.jurusan = ''
    form.value.kelas = ''
    }
}
onMounted(() => {
    getKeanggotaan()
    getKeperluan()
})

</script>
<style scoped>
.content {
    padding-top: 150px;
}

form {
    background-image:linear-gradient(#000000,#000000)  ;
    padding: 1rem;
    border-radius: 20px;
    
    
    
}

.container-fluid {
    background-image: url("@/assets/img/bgbg.jpg");
    background-size:cover;
    width: 100%;
    height: 100vh;
    padding-top: 160px;
}

.btn{
    margin:10px 39%;
}
</style>