<template>
  <section class="review__container" :class="{ open: openState }">
    <header class="review__header">
      <hr class="review-header__decorateLine" />
      <h2 class="review-header__text" v-if="screenWidth < 560">Новый отзыв</h2>
      <h2 class="review-header__text" v-else>Мой отзыв</h2>
      <button
        class="review-header__closeReview"
        @click="$emit('closeReview')"
        type="button"
      ></button>
    </header>
    <hr class="review__decorateLine" />
    <div class="review__wrapper">
      <div class="review__authorInfoContainer">
        <img :src="authorPhotoUrl" alt="photo" class="review__authorPhoto" />
        <div class="review__authorInfo">
          <h2 class="review__reviewTitle">Фоточки в свадебном платьице</h2>
          <p class="review__authorName">Алена Смирнова</p>
        </div>
      </div>
      <ReviewForm @closeReview="$emit('closeReview')" />
    </div>
    <hr class="review__decorateLine" />
    <footer class="review__footer">
      <ActionButton text="Отправить" @click="submitForm" />
    </footer>
  </section>
  <Notification
    v-bind:isHidden="hiddenNotify"
    text="Спасибо, отзыв опубликован!"
    @hideNotify="
      {
        hiddenNotify = true;
      }
    "
  />
</template>

<script>
import ActionButton from "@/components/blocks/actionButton/ActionButton.vue";
import ReviewForm from "@/components/blocks/form/ReviewForm.vue";
import Notification from "@/components/blocks/notification/Notification.vue";
export default {
  name: "review",
  props: {
    openState: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      screenWidth: "",
      authorPhotoUrl: "./img/724cropBig1.jpg",
      hiddenNotify: true
    };
  },
  created() {
    window.addEventListener("resize", this.updateWidth);
    this.updateWidth();
  },
  methods: {
    updateWidth() {
      this.screenWidth = window.innerWidth;
    },
    submitForm() {
      this.$emit("closeReview");
      this.showNotify();
    },
    showNotify() {
      this.hiddenNotify = false;
      setTimeout(() => (this.hiddenNotify = true), 2000);
    }
  },
  emits: ["closeReview"],
  unmounted() {
    window.removeEventListener("resize", this.updateWidth);
  },
  components: { ActionButton, ReviewForm, Notification }
};
</script>

<style scoped lang="scss">
@import "@/components/review/review.scss";
</style>
