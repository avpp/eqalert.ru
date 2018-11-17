<template>
  <img src="../assets/img/question-circle.png" alt="Описание." class="description-icon" v-b-popover.hover.click.blur.left="value" />
</template>
<script>
export default {
  props: ['value']
}
</script>
<style>
.description-icon {
  cursor: pointer;
}
</style>
