<template>
  <div>
    <div>aiueo</div>
    <ChangeLogCard
      v-if="isShow"
      :title="changeLogTitle"
      :message="changeLogMessage"
      @close="onCardClosed"
    />
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: false,
});

const isShow = ref(true);
const changeLogTitle = ref('【2025.4.12変更】');
const changeLogMessage = ref(
  '文章を変更しています。詳細は変更履歴を確認ください。<a href="https://www.google.com" target="_blank">変更履歴</a>',
);

const onCardClosed = () => {
  isShow.value = false;
  console.log('カードを閉じました');
};
</script>
