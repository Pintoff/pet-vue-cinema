<script setup>
import { ref } from 'vue'
import { cinemas } from '../mock';
import Cinema from './Cinema.vue';
import Review from './Review.vue';

const selectedCinema = ref(cinemas[0]);

function selectCinema(cinema) {
  selectedCinema.value = cinema;
}

const addReview = (review) => {
    selectedCinema.value.reviews.push(review);
}

const getLastIdReview = (reviews) => {
    if (reviews.length === 0) {
        return 1;
    }
    return reviews[length - 1] + 1;
}

    
</script>

<template>
  <div class="cinema_tabs">
    <div class="cinema_tab">
        <button @click="selectCinema(cinema)" 
            :disabled="selectedCinema.id == cinema.id"
            v-for="cinema in cinemas" :key="cinema.id">
          {{ cinema.name }}
        </button>
    </div>
  </div>
  <div v-if="selectedCinema">
      <Cinema :cinema="selectedCinema"/>
  </div>
  <div class="reviews_wrap" v-if="selectedCinema.reviews.length != 0">
        <h4>Отзывы</h4>
        <div class="reviews">
          <p v-for="review in selectedCinema.reviews" :key="review.id">
            {{ review.text }} 
            <button>{{ review.rating }} &#9733; </button>
          </p>
        </div>
      </div>
  <div class="no_reviews" v-else>
        <h3>Нет отзывов!</h3>
      </div>
  <Review :maxRating="5"
    :id="getLastIdReview(selectedCinema.reviews)"
    @add-review="addReview"/>

</template>
