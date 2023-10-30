<template>
  <div style="max-width: 300px;width: auto;margin-left: auto;margin-right: auto; margin-top: 3px;"><input v-model="input"
      class="input is-warning" type="text" placeholder="Enter name"> </div>
  <header>
    The Rick and Morty
  </header>
  <main>

    <CardHero v-for="card in cardsInfo" :cardInfo="card" />

    <div style="max-width: 300px;width: auto;margin-left: auto;margin-right: auto;" v-for="card in cardsInfo.slice(0, 1)">
      <el-pagination small background @click="drawCards" v-model:current-page="page" layout="prev, pager, next"
        v-model:total="card.total" />
    </div>
  </main>
</template>

<script setup>
import axios from 'axios'
import { ref, watch, onMounted } from 'vue'
import CardHero from './components/CardHero.vue';

const cardsInfo = ref([])
const input = ref("Rick")
watch(input, () => {
  drawCards()
})
const page = ref()
function drawCards() {
  const inp = input.value
  const pag = page.value
  axios.get(`https://rickandmortyapi.com/api/character/?page=${pag}&name=${inp}`).then((res) => {
    console.log(res.data)
    const tempData = res.data.results.map((item, index) => {
      return {
        total: res.data.info.pages * 10,
        image: res.data.results[index].image,
        name: res.data.results[index].name,
        status: res.data.results[index].status,
        species: res.data.results[index].species,
        location: res.data.results[index].location.name,
        gender: res.data.results[index].gender,
        id: res.data.results[index].id
      }

    })
    cardsInfo.value = tempData
  })
}
// window.onload = function () {
//   drawCards()
// }
onMounted(() => drawCards())
</script>



