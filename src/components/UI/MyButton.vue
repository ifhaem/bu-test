<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
}
</script>

<style scoped lang="scss">
@import 'src/styles/_variables.scss';
.btn {
  padding: 10px;
  justify-content: center;
  background-color: $darkyellow;
  color: $brown;
  border: 1px solid $borderyellow;
  border-radius: 2em;
  &:hover {
    cursor: pointer;
    background-color: $borderyellow;
  }
}
</style>