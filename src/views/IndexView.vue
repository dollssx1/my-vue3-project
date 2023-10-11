<script setup>
import { ref, reactive, onMounted, computed } from 'vue'
import axios from 'axios'

const val1 = ref('')
const txt1 = ref('')
const data = ref()

const val2 = computed(async () => {
  //axios로직  https://fakestoreapi.com/products/1
})

const modData = () => {
  if (data?.value?.id === 1) {
    console.log(data)
  }
}

const fetchData = async () => {
  try {
    const res = await axios.get('https://fakestoreapi.com/products/1')
    data.value = await res?.data
  } catch (error) {
    console.error('An error occurred while fetching data:', error)
  }
}

onMounted(async () => {
  await fetchData()
  modData()
  val1.value = '무식한놈'
})
</script>

<template>
  <BaseInput v-model.capitalize="txt1" />
  <h3>{{ txt1 }}</h3>
  <div v-if="!!data">
    <div>{{ data.id }} : {{ data.title }}</div>
  </div>
</template>
