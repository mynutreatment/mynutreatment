<template>
  <footer>
    <img src="../assets/icons/white-logo.svg" alt="logo" class="logo" width="200" height="200">
    <div class="container">
      <div>
        <h3>Μάθετε περισσότερα</h3>
          <ul>
              <li>
                  <NuxtLink to="/">Αρχική</NuxtLink>
              </li>
              <li>
                  <NuxtLink to="/services">Υπηρεσίες</NuxtLink>
              </li>
              <li>
                  <NuxtLink to="/about">Σχετικά με εμάς</NuxtLink>
              </li>
              <li>
                  <NuxtLink to="/blog">Blog</NuxtLink>
              </li>
              <li>
                  <NuxtLink to="/contact">Επικοινωνία</NuxtLink>
              </li>
          </ul>
      </div>
      <div>
        <h3>Επικοινωνία</h3>
        <ul>
          <li>
            <img src="/assets/icons/Call.svg" alt="">
            <a :href="`tel:${data.phone}`">{{ data.phone }}</a>
          </li>
          <li>
            <img src="/assets/icons/Paper-Plane.svg" alt="">
            <a :href="`mailto:${data.email}`">{{data.email}}</a>
          </li>
          <li>
            <img src="/assets/icons/Facebook.svg" alt="">
            <a :href="data.facebook" target="_blank" class="facebook">Διατροφολόγος - Διαιτολόγος <span>Ιωάννα Παπατζανή</span></a>
          </li>
          <li>
            <img src="/assets/icons/Instagram.svg" alt="">
            <a :href="data.instagram" target="_blank">mynutreatment</a>
          </li>
        </ul>
        <!-- <a href="https://" target="_blank" rel="noopener noreferrer"></a> -->
      </div>
      <img src="../assets/icons/wheat-stems.svg"  alt="wheat-stacks" class="wheat">
      <!-- <img loading="lazy" src="../assets/icons/wheat-stems.svg"  alt="wheat-stacks" class="wheat"> -->
    </div>
    <!-- <NuxtLink to="/credits" class="credits">credits</NuxtLink> -->
    <NuxtLink to="/privacy-policy" class="credits">Πολιτική Απορρήτου</NuxtLink>
  </footer>
</template>

<script lang="ts" setup>
const {data} = await useAsyncData('contact', async () => {
    return await queryContent('main/contact/contact').findOne();
})
</script>

<style scoped>
footer {
  position: relative;
  background-color: var(--dark-brown);
  color: var(--pure-white);
  border-top-left-radius: var(--radius-md);
  border-top-right-radius: var(--radius-md);
  display: flex;
  padding: 1rem;
  padding-block: 4rem;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  overflow-x: clip;
  margin-inline: auto;
  margin-top: 10rem;
  max-width: calc(var(--max-width) + 8rem);
}

.logo {
  padding-block: 2rem;
  border-right: .2rem solid var(--pure-white);
}

.container {
  display: flex;
  gap: 6rem;

}

ul {
  padding-left: 0rem;

  li {
    list-style-type: none;
    margin-block: .5rem;
    display: flex;
    gap: 0.5rem;
    align-items: center
  }
} 

footer:deep(a) {
  color: inherit;
  text-decoration: none;
  transition: opacity 0.2s ease-in;

  &:hover {
    opacity: 0.8;
  }

  &.facebook {
    display: flex;
    flex-direction: column;
    text-align: start;

    /* span {
      font-size: smaller;
    } */
  }
}

.wheat {
  position: absolute;
  /* bottom: -6rem; */
  top: -8rem;
  right: -1rem;
  max-width: 20rem;
  /* max-height: 24rem; */
}


.credits {
  position: absolute;
  bottom: 1rem;
  right: 1rem;
  opacity: .7;
  font-size: smaller;
}

@media screen and (max-width: 767px) {
  footer {
    flex-direction: column;
    justify-content: center;
    text-align: center;

    .container {
      gap: 2rem;
      flex-direction: column;
    }

    ul {
      display: grid;
      justify-items: center;
    }
  }

  .logo {
    /* padding-block: 2rem; */
    border-right: 0rem;
    border-bottom: .2rem solid var(--pure-white);
  }

  .wheat {
    max-width: 13rem;
  }

  /* .credits {
    position: absolute;
    bottom: 2rem;
    right: unset;
  } */
}
</style>