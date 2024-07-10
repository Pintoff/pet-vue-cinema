<script setup>
import Film from './Film.vue';

const props = defineProps({
    cinema: Object
})
console.log(props.cinema);
</script>

<template>
    <h3>{{ cinema.name }}</h3>
      <div class="films_wrap" v-if="cinema.films.length != 0">
        <h4>Фильмы</h4>
        <div class="films" v-for="film in cinema.films" :key="film.id">
          <Film :filmName="film.name" />
        </div>
      </div>
      <div class="no_films" v-else>
        <h3>Нет фильмов!</h3>
      </div>
</template>

<style scoped>
</style>