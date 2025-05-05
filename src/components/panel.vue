<script setup lang="ts">
import Button from "./button.vue";

const { title, description, imgName } = defineProps<{
  title: string;
  description: string;
  imgName: string;
  altImg: string;
}>();
</script>
<template>
  <div class="c-panel">
    <div class="l-panel__grid">
      <div class="l-panel__grid-hero">
        <picture>
          <source
            :srcset="`/images/desktop-image-${imgName}.jpg`"
            media="(width >= 31.25rem)"
          />
          <img
            class="c-panel__hero"
            width="100%"
            height="360"
            :src="`/images/mobile-image-${imgName}.jpg`"
            :alt="altImg"
          />
        </picture>
      </div>
      <div class="l-panel__grid-content">
        <div class="c-panel__body">
          <p class="u-text-heading-1 u-fw-600 u-fc-black">{{ title }}</p>
          <div class="l-panel__description">
            <p class="u-text-body u-fw-500 u-fc-dark-gray">{{ description }}</p>
          </div>
          <Button variant="normal"
            >Shop now
            <svg width="40" height="12" focusable="false">
              <use xlink:href="#icon-arrow" /></svg
          ></Button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped lang="scss">
@use "../scss/functions" as f;

.l-panel {
  &__grid {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 36rem auto;

    @include f.breakpoint(medium) {
      grid-template-rows: 45rem auto;
    }

    @include f.breakpoint(large) {
      grid-template-columns: 84rem 1fr;
      grid-template-rows: 53.4rem;
    }
  }

  &__description {
    padding-top: 1.5rem;
    padding-bottom: 4.1rem;

    @include f.breakpoint(medium) {
      padding-top: 1.65rem;
      padding-bottom: 3.35rem;
    }

    @include f.breakpoint(large) {
      padding-top: 1.8rem;
      padding-bottom: 2.6rem;
    }
  }
}

.c-panel {
  &__hero {
    object-fit: cover;
    object-position: center bottom;

    @include f.breakpoint(medium) {
      height: 45rem;
    }

    @include f.breakpoint(large) {
      height: 53.4rem;
    }
  }

  &__body {
    max-width: 31.1rem;
    margin: 0 auto; /* Center the content */
    padding-top: 6rem;
    padding-bottom: 7.2rem;

    @include f.breakpoint(medium) {
      max-width: 36rem;
      padding-top: 9rem;
      padding-bottom: 10rem;
    }

    @include f.breakpoint(large) {
      max-width: 40rem;
      padding-top: 12rem;
      padding-bottom: 0rem;
    }
  }
}
</style>
