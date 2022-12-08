<script setup>
import { ref, watch } from 'vue'

const searchTerm = ref('');
const terms = ref('');

const findProducts = async term => {
fetch(`https://dummyjson.com/products/search?q=${term}`)
.then(res => 
res.json()
)
.then(
(data) => {
  terms.value = data.products;
  console.log(terms.value)
}
);

}

watch(searchTerm, newTerm => findProducts(newTerm))
</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Gift Search Bar</h1>
    <input type="text" class="p-2 border-2 border-gray-dark" v-model="searchTerm" placeholder="Start typing..." />
    <!-- <div>{{terms}}</div> -->
    <ul class="list-disc" >
      <li v-for="term in terms" :key="term.id">{{term.title}} - ${{term.price}}</li>
      
    </ul>
  </div>
</template>
