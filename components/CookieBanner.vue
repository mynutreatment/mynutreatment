<template>
  <Teleport to="body">
    <Transition name="cookie" appear>
      <section
        v-if="localOpen"
        aria-labelledby="cookie_heading"
        class="default-card default-card-content"
      >
        <h3 id="cookie-heading">Αποδοχή Cookies</h3>
        <p>
          Χρησιμοποιούμε cookies και παρόμοιες τεχνολογίες για να δώσουμε τη
          δυνατότητα σε υπηρεσίες και λειτουργίες στον ιστότοπό μας και να
          κατανοήσουμε την αλληλεπίδρασή σας με την υπηρεσία μας. Κάνοντας κλικ
          στο Αποδοχή, αποδέχεστε τη χρήση τέτοιων τεχνολογιών για το μάρκετινγκ
          και αναλυτικά στοιχεία.
        </p>
        <div>
          <MainButton size="small">
            <button @click="acceptCookies">Αποδοχή</button>
          </MainButton>
          <NuxtLink to="/privacy-policy">Μάθετε περισσότερα</NuxtLink>
        </div>
      </section>
    </Transition>
  </Teleport>
</template>

<script lang="ts" setup>
const props = defineProps<{ open: boolean }>();
const emit = defineEmits(["update:open"]);

watch(
  () => props.open,
  (val) => {
    localOpen.value = val;
  }
);

const localOpen = ref(props.open);

watch(localOpen, (val) => {
  if (!val) emit("update:open", false);
});

function acceptCookies() {
  // localStorage.setItem('cookieBannerAccepted', 'true')
  // localOpen.value = false
}
</script>

<style scoped>
section {
  transform: scale(0.8);
  position: fixed;
  bottom: 1rem;
  right: 1rem;
  z-index: 99;

  background-color: var(--white-semi-transparent);
  backdrop-filter: blur(1rem);
  display: flex;
  flex-direction: column;
  align-items: center;

  h2 {
    width: fit-content;
  }

  p {
    max-height: 7rem;
    overflow-y: scroll;
    mask-image: linear-gradient(
      180deg,
      transparent 0%,
      #000 10%,
      #000 90%,
      transparent 100%
    );
  }

  div {
    display: flex;
    width: 100%;
    justify-content: space-around;
    align-items: center;

    a {
      height: fit-content;
      color: inherit;
      /* background-image: linear-gradient(to bottom, transparent 60%, var(--primary-green) 40%); */
      /* text-decoration: none; */
    }
  }
}
@media screen and (max-width: 767px) {
  section {
    width: 100%;
    max-width: 100vw;
    left: 50%;
    transform: translateX(-50%) scale(0.8);
    bottom: 1rem;
  }
}

.cookie-enter-from,
.cookie-leave-to {
  opacity: 0;
  margin-bottom: -2rem;
}

.cookie-enter-active,
.cookie-leave-active {
  transition: opacity 0.3s, margin-bottom 0.5s;
}
</style>
