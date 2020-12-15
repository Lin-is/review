<template>
  <button class="showReview">Show review</button>
  <Review></Review>
</template>

<script>
import Review from "@/components/review/Review.vue";
export default {
  components: { Review }
};
</script>
<style lang="scss">
@import "@/main.scss";
</style>
