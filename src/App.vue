<template>
  <ActionButton
    text="Показать отзыв"
    class="showReview"
    :class="{ hidden: openReview }"
    @click="
      {
        openReview = true;
      }
    "
  />
  <Review
    v-bind:openState="openReview"
    @closeReview="
      {
        openReview = false;
      }
    "
  ></Review>
</template>

<script>
import Review from "@/components/review/Review.vue";
import ActionButton from "@/components/blocks/actionButton/ActionButton.vue";
export default {
  data() {
    return {
      openReview: false
    };
  },
  components: { Review, ActionButton }
};
</script>
<style lang="scss">
@import "@/main.scss";
</style>
