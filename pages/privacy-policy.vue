<template>
  <div class="prose">
    <ContentRenderer :value="data" />
    
  </div>
</template>

<script lang="ts" setup>
const {data} = await useAsyncData('privacy policy', async () => {
  return await queryContent('main/privacypolicy').findOne();

})
</script>
<style>

</style>