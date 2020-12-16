<template>
  <form action="submit" @submit.prevent class="review__form">
    <div class="review-form__starsContainer">
      <StarsRate
        v-for="(elem, index) of starsInfo"
        :key="index"
        :title="
          index >= 2 && screenWidth < 560 ? 'Исполнитель солнышка?' : elem.title
        "
        :index="index"
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
        @click="$emit('closeReview')"
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
      <input
        type="file"
        id="review-form__photoInput"
        ref="photoInput"
        class="review-form__photoInput"
        accept="image/*"
        @change="downloadPhoto()"
      />
      <lable
        for="review-form__photoInput"
        class="review-form__addPhotoBtn"
        @click="addPhoto"
        :class="{ hidden: addedPhotos.length >= 5 && screenWidth > 559 }"
      ></lable>
      <div
        class="review-form__photoCard"
        v-for="(photo, index) in addedPhotos"
        :key="index"
      >
        <img :src="photo" alt="photo" class="review-form__photo" />
        <button
          class="review-form__photoDeleteButton"
          :data-photo="photo"
          @click="deletePhoto(photo)"
          type="button"
        ></button>
      </div>
    </div>
  </form>
</template>

<script>
import StarsRate from "@/components/blocks/starsRate/StarsRate.vue";
import ActionButton from "@/components/blocks/actionButton/ActionButton.vue";

export default {
  name: "reviewForm",
  data() {
    return {
      screenWidth: "",
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
  emits: ["closeReview"],
  methods: {
    updateWidth() {
      this.screenWidth = window.innerWidth;
      // this.updatePhotos();
    },
    addPhoto() {
      this.$refs.photoInput.click();
    },
    deletePhoto(photo) {
      const photoIndex = this.addedPhotos.indexOf(photo);
      if (photoIndex !== -1) {
        this.addedPhotos.splice(photoIndex, 1);
      }
    },
    downloadPhoto() {
      let downloadedFile = this.$refs.photoInput.files[0];

      let reader = new FileReader();
      reader.addEventListener(
        "load",
        function() {
          this.addedPhotos.push(reader.result);
        }.bind(this),
        false
      );
      if (/\.(jpe?g|png|gif)$/i.test(downloadedFile.name)) {
        reader.readAsDataURL(downloadedFile);
      }
    },
    updatePhotos() {
      if (this.screenWidth) {
        if (this.addedPhotos.length < 5 && this.screenWidth < 560) {
          this.addedPhotos.push("./img/photos/image46_4.jpg");
        } else if (this.addedPhotos.length > 4 && this.screenWidth > 559) {
          this.addedPhotos.splice(4, 1);
        }
      }
    }
  },
  unmounted() {
    window.removeEventListener("resize", this.updateWidth);
  },
  components: {
    StarsRate,
    ActionButton
  }
};
</script>

<style scoped lang="scss">
@import "@/components/blocks/form/form.scss";
</style>
