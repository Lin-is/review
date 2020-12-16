<template>
  <div class="starsRate__container">
    <p class="starsRate__title">{{ title }}</p>
    <div class="starsRate__starsContainer">
      <input
        type="radio"
        :name="`${title}-rating-${index}`"
        class="starsRate__starInput"
        :id="`${title}-rating-${index}-5`"
        v-bind:value="5"
        :checked="value === 5"
      />
      <label
        class="starsRate__star"
        :for="`${title}-rating-${index}-5`"
        v-bind:value="5"
      ></label>
      <input
        type="radio"
        :name="`${title}-rating-${index}`"
        class="starsRate__starInput"
        :id="`${title}-rating-${index}-4`"
        v-bind:value="4"
        :checked="value === 4"
      />
      <label
        class="starsRate__star"
        :for="`${title}-rating-${index}-4`"
        v-bind:value="4"
      ></label>
      <input
        type="radio"
        :name="`${title}-rating-${index}`"
        class="starsRate__starInput"
        :id="`${title}-rating-${index}-3`"
        v-bind:value="3"
        :checked="value === 3"
      />
      <label
        class="starsRate__star"
        :for="`${title}-rating-${index}-3`"
        v-bind:value="3"
      ></label>
      <input
        type="radio"
        :name="`${title}-rating-${index}`"
        class="starsRate__starInput"
        :id="`${title}-rating-${index}-2`"
        v-bind:value="2"
        :checked="value === 2"
      />
      <label
        class="starsRate__star"
        :for="`${title}-rating-${index}-2`"
        v-bind:value="2"
      ></label>
      <input
        type="radio"
        :name="`${title}-rating-${index}`"
        class="starsRate__starInput"
        :id="`${title}-rating-${index}-1`"
        v-bind:value="1"
        :checked="value === 1"
      />
      <label
        class="starsRate__star"
        :for="`${title}-rating-${index}-1`"
        v-bind:value="1"
      ></label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    rate: {
      type: Number,
      required: false
    },
    index: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      value: 1
    };
  },
  mounted() {
    this.value = this.rate | 0;
  },
  watch: {
    value: function() {
      this.$emit("rateValue", {
        index: this.index,
        title: this.title,
        value: this.value
      });
    }
  }
};
</script>

<style scoped lang="scss">
@import "@/components/blocks/starsRate/starsRate.scss";
</style>
