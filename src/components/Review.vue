<template>
    <div class="user_review">
        <label for="review">Ваш отзыв:</label>
        <input type="text" name="review" id="" v-model="text">
        <div class="rating_box" >
          <h4>Насколько вы оцениваете кинотеатр?</h4>
          <button v-for="rate in maxRating" 
          :key="rate"
          @click="chooseRating(rate)">
            {{ rate }} &#9733;</button>
        </div>
        <button @click="addReview">Добавить отзыв</button>
    </div>
</template>

<script setup>
  import {ref} from 'vue'
  const props = defineProps({maxRating : Number});
  const emits = defineEmits(['add-review', ]);
  const text = defineModel('text');
  const rating = ref(1);
  const addReview = () => {
    emits('add-review', {id: 4, rating: rating.value, text: text.value});
    text.value = '';
  }

  function chooseRating(rate) {
    rating.value = rate;
  }

  function reset() {
    text.value = '';
  }
</script>

<style scoped>

</style>