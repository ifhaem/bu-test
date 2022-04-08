<template>
    <div class="beer">
      <div class="beer__brand">{{ this.beer.brand }}</div>
      <div class="beer__name">{{ this.beer.name }}</div>
      <div class="beer__alc">Alcohol: {{ this.beer.alcohol }}</div>
    </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  components: {MyButton},
  props: {
    beer: {
      brand: String,
      name: String,
      alcohol: String
    }
  },
}
</script>

<style scoped lang="scss">
@import 'src/styles/_variables.scss';
.beer {
  display: flex;
  flex-direction: column;
  &__brand {
    font-size: 2em;
    text-align: center;
  }
  &__name, &__alc {
    margin-left: 10px;
  }
  &>* {
    margin-top: 10px;
  }
}
</style>