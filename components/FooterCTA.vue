<template>
  <section>
    <NuxtPicture
      :src="footer.image"
      :alt="footer.alt"
      width="550"
      height="450"
      sizes="sm:800"
      placeholder
      fit="cover"
      loading="lazy"
    />
    <div class="text">
      <h2>
        {{ footer.description }}
      </h2>
      <MainButton size="large" class="btn">
        <NuxtLink to="/contact">Κλείστε ραντεβού</NuxtLink>
      </MainButton>
    </div>
  </section>
</template>

<script lang="ts" setup>
const footer = await queryContent("main/footercta").findOne();
</script>

<style scoped>
section {
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
  padding: 1rem;
  margin-top: 4rem;
}

picture {
  /* width: 100%; */
  justify-self: end;
  margin-right: -2rem;
  transform: translateX(2rem);

  &:deep(img) {
    object-fit: contain;
  }
}

.text {
  display: grid;
  gap: 2rem;
  max-width: 35rem;
}

h2 {
  /* text-align: justify; */
  font-size: var(--header-xl);
  font-weight: 600;
  color: var(--white);
  letter-spacing: 0.2rem;
  -webkit-text-stroke: 0.12rem var(--dark-blue);
}

.btn {
  justify-self: end;
  margin-right: 3rem;
}

@media screen and (max-width: 767px) {
  section {
    grid-template-columns: 1fr;
    justify-items: center;
    /* width: 100vw; */
    /* text-align: center; */
    padding: unset;
  }

  h2 {
    /* text-align: justify; */
    font-size: calc(var(--header-xl) - 0.7rem);
    font-weight: 600;
    color: var(--white);
    letter-spacing: 0.1rem;
    -webkit-text-stroke: 0.08rem var(--dark-blue);
    margin-left: 1rem;
  }

  .text {
    align-self: start;
  }

  picture {
    justify-self: center;
    margin-right: 0rem;
    /* order: 2; */

    &:deep(img) {
      /* object-fit: contain; */
      /* fixed alignment for tiny screens */
      object-position: bottom;
    }
  }
}
</style>
