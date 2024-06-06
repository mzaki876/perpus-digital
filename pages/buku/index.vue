<template>
  <div class="wrapper">
    <div class="content"></div>
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <nuxt-link to="/pengunjung">
          <button type="button" class="btn btn-outline-dark mt-4 btn-lg">KEMBALI</button></nuxt-link>
          <h2 class="text-center my-4 text-light">RAK BUKU</h2>
          <form @submit.prevent="getBooks">
            <input v-model="keyword" type="search" class="form-control form-control-lg rounded-5" placeholder="Cari..." >
          </form>
        <div class="my-3 text-light">menampilkan {{ bookFiltered.length }} dari {{ bookFiltered.length }}</div>
          <div class="row">
              <div v-for="(book,i) in bookFiltered" :key="i" class="col-lg-2">
                  <div  class="card cb mb-3">
                    <div class="card-body">
                        <nuxt-link :to="`/buku/${book.id}`">
                        <img :src="book.cover" class="cover" :alt="book.judul">
                      </nuxt-link>
                    </div>
                  </div>
              </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
const supabase= useSupabaseClient ()

const books = ref([])
const kategories = ref([])
const keyword = ref('')

const getBooks = async () => {
  const { data ,error } = await supabase
  .from('buku')
  .select(`*, kategori(*)`)
  .ilike("judul", `%${keyword.value}`)
  .order('id')
  if(data) books.value = data
}

async function getKategori(){
  const{data, error} = await supabase.from('kategori_buku')
  .select('*')
  if(data) kategories.value = data
}

const bookFiltered = computed (() => {
  return books.value.filter((b) => {
      return (
          b.judul?.toLowerCase().includes(keyword.value?.toLowerCase()) ||
          b.kategori?.nama.toLowerCase().includes(keyword.value?.toLowerCase())
      )
  })
}) 

onMounted(() =>{
  getBooks()
})
</script>
<style scoped>
.content{
  background-image: url("@/assets/img/bg.jpg");
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
.card-body {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
  padding: 0;
}
.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}
.btn{
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: #ffffff;
  color: black;
  width: 150px;
  height: 50px;
  /* margin-top: 60px; */
}

.cb{
  background-color: #ffffff;
  border: 0;
  height: 250px;
  width: 180px;
  margin: 5px 5px;
}

.container-fluid {
  padding-top: 170px;
    background-size:cover;
    
}

</style>