<template>
  <section class="review__container" :class="{ open: openState }">
    <header class="review__header">
      <hr class="review-header__decorateLine" />
      <h2 class="review-header__text" v-if="screenWidth < 560">Новый отзыв</h2>
      <h2 class="review-header__text" v-else>Мой отзыв</h2>
      <button
        class="review-header__closeReview"
        @click="closeReview"
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
      <form action="submit" @submit.prevent class="review__form">
        <div class="review-form__starsContainer">
          <StarsRate
            v-for="(elem, index) of starsInfo"
            :key="index"
            :title="
              index >= 2 && screenWidth < 560
                ? 'Исполнитель солнышка?'
                : elem.title
            "
            :rate="elem.rate"
          />
        </div>

        <footer class="review-form__middleFooter">
          <hr class="review-form__footerDecoration" />
          <ActionButton text="Продолжить" />
        </footer>

        <header class="review-form__middleHeader">
          <h2 class="review-header__text">Новый отзыв</h2>
          <button
            class="review-header__closeReview"
            @click="closeReview"
            type="button"
          ></button>
          <hr class="review-header__decorateLine" />
        </header>

        <div class="review-form__commentContainer">
          <textarea
            class="review-form__comment"
            name="review-form__comment"
            id="review-form__textarea"
            placeholder="Комментарий "
          ></textarea>
          <label for="review-form__textarea" class="review-form__counter">
            12/500
          </label>
        </div>
        <div class="review-form__photoContainer">
          <button class="review-form__addPhotoBtn" type="button"></button>
          <div
            class="review-form__photoCard"
            v-for="(photo, index) in addedPhotos"
            :key="index"
          >
            <img :src="photo" alt="photo" class="review-form__photo" />
            <button
              class="review-form__photoDeleteButton"
              type="button"
            ></button>
          </div>
        </div>
      </form>
    </div>
    <hr class="review__decorateLine" />
    <footer class="review__footer">
      <ActionButton text="Отправить" />
    </footer>
  </section>
</template>

<script>
import ActionButton from "@/components/blocks/actionButton/ActionButton.vue";
import StarsRate from "@/components/blocks/starsRate/StarsRate.vue";
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
      starsInfo: [
        {
          title: "Скорость",
          rate: 3
        },
        {
          title: "Скорость отдачи видео"
        },
        {
          title: "Качество"
        },
        {
          title: "Пунктуальность"
        }
      ],
      addedPhotos: [
        "./img/photos/image46_0.jpg",
        "./img/photos/image46_1.jpg",
        "./img/photos/image46_2.jpg",
        "./img/photos/image46_3.jpg"
      ]
    };
  },
  created() {
    window.addEventListener("resize", this.updateWidth);
    this.updateWidth();
  },
  methods: {
    updateWidth() {
      this.screenWidth = window.innerWidth;
      this.updatePhotos();
    },
    updatePhotos() {
      if (this.screenWidth) {
        if (this.addedPhotos.length < 5 && this.screenWidth < 560) {
          this.addedPhotos.push("./img/photos/image46_4.jpg");
        } else if (this.addedPhotos.length > 4 && this.screenWidth > 559) {
          this.addedPhotos.splice(4, 1);
        }
      }
    },
    closeReview() {
      this.$emit("closeReview");
    }
  },
  unmounted() {
    window.removeEventListener("resize", this.updateWidth);
  },
  components: { ActionButton, StarsRate }
};
</script>

<style scoped lang="scss">
@import "@/components/review/review.scss";
</style>
