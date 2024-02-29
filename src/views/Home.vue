<template>
    <div class="flex flex-col p-8 ">
        
        <div class="flex gap-2 justify-center">
            <router-link :to="{name: 'byLetter',params:{letter}}" v-for="letter of letters.split('')" :key="letter">
                {{ letter }}
            </router-link>
        </div>
    </div>
</template>

<script setup>
import axiosClient from '../axiosClient';
import store from '../store';
import { computed, onMounted, ref } from 'vue'

const meals = computed(() => store.state.meals);
const letters = 'ABCDEFGHIJKLMNOPQLSTUVWXYZ';
const ingredients=ref([])


onMounted(async()=>{
    const response=await axiosClient.get('/list.php?i=list');
    console.log(response.data)
    ingredients.value=response.data;
})
</script>