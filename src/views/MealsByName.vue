<template>
    <div class="p-8 pb-0">
        <input 
        type="text" 
        v-model="keyword"
        class="rounded border-2 border-gray-200 w-full" 
        placeholder="Search for meals"
        @change="SearchMeals"
        />
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
        <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
            <router-link :to="{name:'mealDetails',params:{id:meal.idMeal}}">
                <img :src="meal.strMealThumb" alt="strMeal" class="rounded-t-xl h-48 object-cover w-full">
            </router-link>
            <div class="p-3">
                <h3 class="font-bold">{{ meal.strMeal }}</h3>
            <p class="mb-4">Lorem ipsum dolor sit amet consectetur adipisicing elit. Hic vitae voluptate consequuntur quaerat perferendis quod accusamus harum consequatur expedita! Eum repudiandae, quae, consectetur, animi illo adipisci saepe iste minus dolorum explicabo nam fugiat. Nemo, eveniet sed. Exercitationem maxime facilis esse eaque aut sunt natus consequatur et voluptatum reprehenderit expedita, ad omnis accusantium vitae voluptatibus libero fuga obcaecati nesciunt ipsum dolore.</p>
            <div class="flex items-center justify-between">
                <a :href="meal.strYoutube" target="_blank" class="px-3 py-2 text-white rounded border-red-600 border-2 bg-red-500 hover:bg-red-600 transition-colors">YouTube</a>
            </div>
            </div>
            
        </div>
    </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
import store from '../store';
import {ref,computed, onMounted} from 'vue';
import { searchMeals } from '../store/actions';


const route=useRoute();
const keyword= ref("");
const meals=computed(()=>store.state.searchedMeals)
function SearchMeals(){
    store.dispatch('searchMeals',keyword.value )
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword) {
    SearchMeals()
  }

})

</script>