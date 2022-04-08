<template>
  <div class="navbar">
    <div class="navbar__title">BEERandomiser</div>
    <my-button @click="$emit('new-user')" class="navbar__btn">Другой пользователь</my-button>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  components: {MyButton}
}
</script>

<style lang="scss">
@import 'src/styles/_variables.scss';
.navbar {
  height: 50px;
  background-color: $brown;
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__title {
    color: $yellow;
    font-weight: bold;
    margin-left: 10vw;
  }
  &__btn {
    margin: 5px 10vw 5px 5px;
  }
}
</style>