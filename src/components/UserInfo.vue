<template>
  <div class="user">
    <img class="user__image" :src="this.user.photoUrl">
    <div class="user__name">{{ this.user.name }}</div>
    <div class="user__work">Work position: {{ this.user.workPosition }}</div>
    <div class="user__age">Age: {{ this.user.age }}</div>
  </div>
</template>

<script>
export default {
  props: {
    user: {
      name: String,
      workPosition: String,
      age: String,
      photoUrl: String
    }
  },
}
</script>

<style scoped lang="scss">
@import 'src/styles/_variables.scss';
.user {
  display: flex;
  flex-direction: column;
  width: 300px;
  border: 2px solid $brown;
  border-radius: 10px;
  &__image {
    border: 1px solid $borderyellow;
    min-height: 300px;
  }
  &__name {
    font-size: 2em;
    text-align: center;
    margin: 0 10px;
  }
  &__work, &__age {
    margin: 10px;
  }
  &__age {
    margin-top: 0;
  }
}
</style>