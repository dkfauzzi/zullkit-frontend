<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import CategoriesCard from './../CategoriesCard.vue';

const categories = ref([])

async function getCategoriesData(){
  try{
      const response = await axios.get('http://127.0.0.1:8000/api/categories?show_product=1');
      console.log(response.data);
      categories.value = response.data.data.data
  } catch (error) {
    console.error(error)
  }
}


onMounted(() =>{
  getCategoriesData()
})

</script>
<template>
  <div class="container px-4 mx-auto my-16 md:px-12" id="categories">
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">Top Categories</h2>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <CategoriesCard v-for="categories in categories" 
      :key="categories.id" 
      :title="categories.name"
      :image="categories.thumbnails" 
      :count="categories.products_count.length" />
    </div>
  </div>
</template>