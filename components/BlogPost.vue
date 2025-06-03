<script lang="ts" setup>

const props = defineProps<{
  post: {
    type: Object,
    required: true,

    title: string,
    image: string,
    credit: string,
    alt: string,
    author: string,
    authorImage: string,
    authorLink: string
  }
}>()

const url = computed(() => {
  // return `url(${props.post.image})`
  const img = useImage()
  const imgUrl = img(props.post.image, { width: 200 })
  return `url('${imgUrl}')`
})


let shareResult = ref("")
const copyURL = (async() => {
  console.log()

  const shareData = {
    title: props.post.title,
    url: window.location.href
  }
  
  if(!navigator.canShare) {
    navigator.clipboard.writeText(shareData.url)
    shareResult.value = "Link copied!"

    // setTimeout(() => {
    //   shareResult.value = "", 200
    // })
  }
  else {
    try {
      await navigator.share(shareData)
    }
    catch(err) {
      console.log(err)
    }
  }
})
</script>

<template>
  <article class="blog-post">
      <header>
        <div class="img-wrapper" :data-credit="post.credit">
          <NuxtPicture :src="post.image" :alt="post.alt"  width="886" height="620" sizes="sm:800" placeholder fit="cover" />

          <!-- <img :src="post.image" :alt="post.alt"> -->
        </div>
        <h1>{{ post.title }}</h1>
        <div>
          <address>
            <img :src="post.authorImage" :alt="post.author">
            <a :href="post.authorLink">{{post.author}}</a>
          </address>
          <MainButton size="small">
            <button @click="copyURL">Share</button>
          </MainButton>
          <p v-if="shareResult">{{ shareResult }}</p>
        </div>


        <!-- <ShareButton>SHARE</ShareButton> -->

      </header>
        <div class="prose">
            <ContentRenderer :value="post" />
        </div>
    </article>
</template>


<style scoped>

/* create new component */
address {
  display: inline-flex;
  align-items: center;
  gap: .5rem;

  img {
    max-width: 2.5rem;
    max-height: 3rem;
    border-radius: 50rem;
  }

  a {
    text-decoration: none;
    font-style: normal;
    color: inherit;
  }
} 

/* button {
  appearance: none;
  background-color: inherit;
  border: none;
  cursor: pointer;
} */

article.blog-post {
    --bp-padding: 1rem;
    --bp-top-mg: calc(var(--bp-padding) * 4);

    max-width: 45rem;
    padding: var(--bp-padding);
    margin-top: var(--bp-top-mg);
    margin-inline: auto;
    background-color: var(--pure-white);
    border: var(--card-border);
    border-radius: var(--radius-sm);
    border-top-left-radius: var(--radius-md);
    border-top-right-radius: var(--radius-md);
    

    header {
        display: grid;
        position: relative;
        /* gap: 1.5rem; */
        margin-top: calc(var(--bp-padding) - var(--bp-padding) * 4);
        margin-bottom: 1.5rem;
        /* transform: translateY(-2rem); */
        
        .img-wrapper {
          position: relative;
          filter: drop-shadow(0rem 0.25rem 0.5rem #00000071);


            &::before {
              content: "";
              position: absolute;
              bottom: -0.5rem;
              width: 100%;
              height: 80%;
              background-image: v-bind(url);
              background-position: center;
              background-size: cover;
              filter: blur(1.2rem);
              /* border-radius: calc(var(--radius-md) * 0.75); */
              z-index: -1;

            }

            &::after {
              content: v-bind('post.credit');
              content: attr(data-credit);
              /* content: 'red'; */
              position: absolute;
              right: .75rem;
              bottom: -1.7rem;
              font-size: smaller;
            }



            &:deep(img) {
                position: relative;
                max-height: 27rem;
                height: auto;
                width: 100%;
                object-fit: cover;
                object-position: center;
                border-radius: var(--radius-sm);
                border-top-left-radius: calc(var(--radius-md) * 0.75);
                border-top-right-radius: calc(var(--radius-md) * 0.75);
                /* mask-image: linear-gradient(to top left, red 70%, transparent); */
                filter: drop-shadow(0rem 0.15rem 0.15rem #00000071);
                z-index: 2;
            }
        }

    }

    h1 {
      margin-top: 2rem;
      margin-bottom: 1rem;
    }

    h1 + div {
      display: flex;
      align-content: center;

      address {
        margin-right: auto;
      }

      & p {
        position: absolute;
        right: 0;
        bottom: -2rem;
      }
    }

    h1, address, .prose {
      margin-inline: 1rem;
    }

    /* .prose {
      &:deep(p) {
        padding-block: 0.25rem;
        text-indent: 1rem;

        &:first-of-type {
          text-indent: 0;
        }
      }

      &:deep(h2 + p, h1 + p) {
        text-indent: 0;
      }

      &:deep(img) {
        border-radius: var(--radius-sm);
        margin-block: 0.5rem;
        margin-inline: auto;
      }

      
    } */
    
}

@media screen and (max-width: 767px) {
  article.blog-post {
    margin-inline: -1rem;
  }
}
</style>