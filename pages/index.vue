<template>
  <div id="content">
    <div id="header">
      <h2>Index</h2>
    </div>
    <div id="main">
      <nuxt-link to="/test-001">test-001へ</nuxt-link>
    </div>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: false,
});
</script>

<style lang="scss" scoped>
#content {
  margin: 16px;

  #header {
    margin-bottom: 10px;
  }
}
</style>
