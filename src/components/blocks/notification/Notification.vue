<template>
  <div class="notification__container" :class="{ shown: !isHidden }">
    <p class="notification__text">{{ text }}</p>
    <button
      class="notification__closeBtn"
      @click="$emit('hideNotify')"
    ></button>
  </div>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      required: true
    },
    isHidden: {
      type: Boolean
    }
  },
  emits: ["hideNotify"]
};
</script>

<style scoped lang="scss">
@import "@/components/blocks/notification/notification.scss";
</style>
