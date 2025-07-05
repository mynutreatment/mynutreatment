<template>
  <div class="button" :class="size">
    <slot />
  </div>
</template>

<script lang="ts" setup>
// interface Size {
//   type: "small" | "regular" | "large";
// }

type Size = "small" | "regular" | "large";

const props = defineProps<{
  size?: Size;
}>();
</script>

<style scoped>
.button {
  display: block;
  width: fit-content;
  height: fit-content;
  /* width: fit-content;
  height: fit-content;
  border: var(--border-regular) solid var(--dark-blue); */
  border-radius: var(--radius-lg);
  position: relative;
  cursor: pointer;

  &::after {
    content: "";
    width: 100%;
    height: 100%;
    border-radius: inherit;
    background-color: var(--primary-green);
    position: absolute;
    bottom: -0.4rem;
    right: -0.4rem;
    z-index: 1;
    transition: all 0.3s;
  }

  &:hover::after,
  &:focus-within::after {
    bottom: 0rem;
    right: 0rem;
  }

  &.small {
    font-size: smaller;
  }

  &.large {
    font-size: larger;
  }

  &:deep(a),
  &:deep(button) {
    text-decoration: none;
    color: inherit;
    background-color: inherit;
    display: inline-block;
    padding-inline: 1rem;
    padding-block: 0.5rem;
    width: fit-content;
    height: fit-content;
    border: var(--border-regular) solid var(--dark-blue);
    border-radius: inherit;
    appearance: none;
    cursor: pointer;
    position: relative;
    z-index: 2;

    &:focus-visible {
      outline: none;
    }
  }
}
</style>
