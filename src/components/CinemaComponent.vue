<script>
import { ref, reactive } from 'vue'
import { cinemas } from '../mock';
import  Film  from './Film.vue';
import Review from './Review.vue';


export default {
  components: {
    Film, Review
  },
  setup() {
    const count = ref(0)
    const data = reactive(cinemas);
    const selectedCinema = ref(cinemas[0]);
    function selectCinema(cinema) {
        selectedCinema.value = cinema;
    }
    
    const addReview = (review) => {
      console.log(selectedCinema.value);
      console.log('add review');
      selectedCinema.value.reviews.push(review);
    }

    return {
      count, cinemas, selectedCinema, selectCinema, addReview
    }
  },

  mounted() {
    console.log(this.count) // 0
    console.log(cinemas);
  }


}
</script>

<template>
  <div class="cinema_tabs">
    <div class="cinema_tab">
        <button @click="selectCinema(cinema)" 
        :disabled="selectedCinema.id == cinema.id"
        v-for="cinema in cinemas" :key="cinema.id">
          {{ cinema.name }}</button>
    </div>
  </div>
  <div v-if="selectedCinema">
      <h3>{{ selectedCinema.name }}</h3>
      <div class="films_wrap" v-if="selectedCinema.films.length != 0">
        <h4>Фильмы</h4>
        <div class="films" v-for="film in selectedCinema.films" :key="film.id">
          <Film :film="film" />
        </div>
      </div>
      <div class="no_films" v-else>
        <h3>Нет фильмов!</h3>
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
      @add-review="addReview"/>
  </div>
  

</template>