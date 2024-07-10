<script setup>
import { ref } from 'vue';

const count = ref(0);

const props = defineProps(
  {
    filmName : String,
    required: true,

  }
)

function setCount(num) {
  count.value = num;
}

</script>

<template>
    <div class="film_item">
        {{ filmName }}
        <button @click="setCount(count - 1)" :disabled="count === 0">-</button>
        {{ count }}
        <button @click="setCount(count + 1)" :disabled="count > 5">+</button>
    </div>
</template>

