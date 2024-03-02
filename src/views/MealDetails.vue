<template>
    <div>
        <pre>{{ meal }}</pre>
        <!-- <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1> -->
        <!-- <img :src="meal[0].strMealThumb" :alt="meal.strMeal"> -->
    </div>
</template>

<script setup>
import { ref,onMounted } from 'vue';
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';

const route=useRoute();
const meal=ref({});


onMounted(()=>{
    axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({data})=>{
        // debugger;
        meal.value=data.meals[0]
    })
})
</script>