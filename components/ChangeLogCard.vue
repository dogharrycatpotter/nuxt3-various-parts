<template>
  <div
    v-if="visible"
    :class="['changelog-card', animationClass]"
    @animationend="onAnimationEnd"
  >
    <div class="changelog-card-notice">
      <div>
        <p>{{ title }}</p>
        <span
          id="close-btn"
          @click="hideCard"
          >&times;</span
        >
      </div>
      <p
        id="message-area"
        v-html="message"
      ></p>
    </div>
  </div>
</template>

<script setup lang="ts">
const visible = ref(true);
const animationClass = ref('show');

withDefaults(
  defineProps<{
    title: string;
    message: string;
  }>(),
  {
    title: '',
    message: '',
  },
);

const emits = defineEmits<{
  close: [];
}>();

const hideCard = () => {
  animationClass.value = 'hide';
  setTimeout(() => {
    emits('close');
  }, 600);
};

const onAnimationEnd = () => {
  if (animationClass.value === 'hide') {
    visible.value = false;
  }
};
</script>

<style lang="scss" scoped>
.changelog-card {
  position: fixed;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1000;
  width: 100%;
  height: 120px;
  font-family: sans-serif;
  color: #333;
  background: #fff;
  border-radius: 16px 16px 0 0;
  box-shadow: 0 -4px 12px rgba(0, 0, 0, 0.15);

  &.show {
    animation: slideUpFadeIn 0.6s ease-out forwards;
  }

  &.hide {
    animation: slideDownFadeOut 0.6s ease-in forwards;
  }

  .changelog-card-notice {
    padding: 14px;

    div {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 0 0 6px;
      font-size: 16px;
      font-weight: bold;
    }

    ul {
      padding-left: 20px;
      margin: 0;
      font-size: 14px;
    }
  }

  #close-btn {
    font-size: 20px;
    color: #bbb;
    cursor: pointer;

    &:hover {
      color: #555;
    }
  }
}

@media screen and (min-width: 960px) {
  .changelog-card {
    max-width: 960px;
    margin: 0 auto;
  }
}

@keyframes slideUpFadeIn {
  from {
    opacity: 0;
    transform: translateY(100%);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideDownFadeOut {
  from {
    opacity: 1;
    transform: translateY(0%);
  }
  to {
    opacity: 0;
    transform: translateY(100%);
  }
}
</style>

<style lang="scss">
#message-area {
  a {
    text-decoration: underline;
  }
}
</style>
