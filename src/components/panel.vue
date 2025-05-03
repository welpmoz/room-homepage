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
  <div>
    <picture>
      <source
        :srcset="`/images/desktop-image-${imgName}.jpg`"
        media="(width >= 700px)"
      />
      <img :src="`/images/mobile-image-${imgName}.jpg`" :alt="altImg" />
    </picture>
    <div>
      <h3 class="u-text-heading-1 u-fw-600 u-fc-black">{{ title }}</h3>
      <p class="u-text-body u-fw-500 u-fc-dark-gray">{{ description }}</p>
      <Button variant="normal"
        >Shop now
        <svg width="40" height="12" focusable="false">
          <use xlink:href="#icon-arrow" /></svg
      ></Button>
    </div>
  </div>
</template>
