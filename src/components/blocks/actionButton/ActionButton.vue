<template>
  <button class="actionButton__body">{{ text }}</button>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      required: true
    }
  }
};
</script>

<style scoped lang="scss">
@import "@/components/blocks/actionButton/actionButton.scss";
</style>
