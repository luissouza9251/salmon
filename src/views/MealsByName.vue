<template>
  <div class="p-8 pb-0">
    <input type="text" v-model="keyword" class="rounded border-2 border-gray-200  w-full" placeholder="Search for Meals"
      @change="searcheMeals" />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div v-for="meal of meals" :key="meal.idMeal" 
      class="bg-white shadow  
      rounded-rounded-xl"
    >

      <router-link :to="{name:'mealDetails', params: {id: meal.idMeal}}" >

        <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t w-full h-48  object-cover">

      </router-link>

      <div class="p-3">

        <h3 class="font-bold">{{ meal.strMeal }}</h3>

        <p class="mb-4">
          Lorem ipsum dolor sit amet,<br> consectetur adipisicing elit. Hic odit, laboriosam perspiciatis ea,<br>
          ullam repellat eveniet veniam.
        </p>
        <div class="flex items-center justify-between">
          <YouTubeButton :href="meal.strYoutube" />
        </div>
        </div>
      </div>
  </div>
</template>


<script setup>
import { computed} from '@vue/reactivity';
import { onMounted, ref } from 'vue';
import  { useRoute } from 'vue-router';
import store from '../store';
import YouTubeButton from '../components/YouTubeButton.vue';


const route = useRoute();
const keyword = ref("");
const meals = computed( () => store.state.searchedMeals);

function searcheMeals() {
  store.dispatch('searchMeals', keyword.value);
}

  onMounted(() => {
   keyword. value =  route.params.nome
    if (keyword.value) {
      searcheMeals()
    }

  })

</script>