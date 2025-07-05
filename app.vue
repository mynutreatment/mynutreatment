<template>
  <SiteHeader />
  <main>
    <NuxtPage />
  </main>
  <CookieBanner />
  <FooterCTA v-if="!isContactPage" />
  <SiteFooter />
</template>
<script setup lang="ts">
useSeoMeta({
  themeColor: "#C6DBC3"
})

useHead({
  htmlAttrs: {
    lang: 'el'
  },
  link: [
    {
      rel: 'icon',
      type: 'image/png',
      href: '/favicon.png'
    }
  ]
})

const route = useRoute();

const isContactPage = computed(() => {
  return route.name === 'contact';
});
</script>
<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.3s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  transform: translateY(1rem) rotateZ(0.0deg);
  filter: blur(1rem);
}


.post-enter-active,
.post-leave-active {
  transition: all 0.5s;

}
.post-enter-from,
.post-leave-to {
  opacity: 0;
  background-color: red;
  border: 4px solid blue;
  transform: translateY(2rem) rotateZ(1deg);
  filter: blur(0rem);

}

@keyframes slidefromleft {
  from {
    transform: translateX(-4rem);
    filter: opacity(0);
  }

  to {
    transform: translateX(0rem);
    filter: opacity(1);
  }
}

@keyframes slidefromright {
  from {
    transform: translateX(4rem);
    filter: opacity(0);
  }

  to {
    transform: translateX(0rem);
    filter: opacity(1);
  }
}

@keyframes slidefromrightabout {
  from {
    transform: translateX(4rem) translateY(8rem);
    filter: opacity(0);
  }

  to {
    transform: translateX(-5rem) translateY(8rem);
    filter: opacity(1);
  }
}

@keyframes slidefromtop {
  from {
    transform: translateY(-4rem);
    filter: opacity(0);
  }

  to {
    transform: translateY(0rem);
    filter: opacity(1);
  }
}

@keyframes slidefrombottom {
  from {
    transform: translateY(4rem);
    filter: opacity(0);
  }

  to {
    transform: translateY(0rem);
    filter: opacity(1);
  }
}

@keyframes opacityfade {
  from {
    filter: opacity(0);
  }

  to {
    filter: opacity(1);
  }
}
</style>