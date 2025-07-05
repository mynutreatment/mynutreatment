<template>
  <article class="prose">
    <ContentRenderer :value="data" />
  </article>
</template>

<script lang="ts" setup>
const {data} = await useAsyncData('privacy policy', async () => {
  return await queryContent('main/privacypolicy').findOne();

})
</script>
<style scoped>
article {
  --bp-padding: 2rem;
  --bp-top-mg: calc(var(--bp-padding) * 2);

  max-width: 45rem;
  padding: var(--bp-padding);
  padding-top: var(--bp-top-mg);
  margin-top: var(--bp-top-mg);
  margin-inline: auto;
  background-color: var(--pure-white);
  border: var(--card-border);
  border-radius: var(--radius-sm);
  border-top-left-radius: var(--radius-md);
  border-top-right-radius: var(--radius-md);
}

</style>