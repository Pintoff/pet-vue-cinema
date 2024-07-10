<script>
import { toRefs, ref } from 'vue';



export default {
  props: {
    film: {
      type: Object,
      required: true
    }
  },
  setup(props) {
    const { film } = toRefs(props);
    var count = ref(0);
    //console.log(film);
    function setCount(num) {
        this.count = num;
    }
    return { film, count, setCount };
  }, 
  mounted() {

  }
}

</script>

<template>
    <div class="film_item">
        {{ film.name }}
        <button @click="setCount(count - 1)" :disabled="count === 0">-</button>
        {{ count }}
        <button @click="setCount(count + 1)" :disabled="count > 5">+</button>
    </div>
</template>

