<script setup lang="ts">
import { ref } from "vue";
import Button from "./button.vue";
import Panel from "./panel.vue";

type CarouselItem = {
  title: string;
  description: string;
  imgName: string;
  altImg: string;
};

const { items } = defineProps<{
  items: CarouselItem[];
}>();

const currentPanel = ref(0);

const changePanel = (newPanelIndex: number) => {
  currentPanel.value = newPanelIndex;
};

const handleNextPanel = () => {
  const nextPanelIndex = (currentPanel.value + 1) % items.length;
  changePanel(nextPanelIndex);
};

const handlePreviousPanel = () => {
  const previousPanelIndex =
    (currentPanel.value - 1 + items.length) % items.length;
  changePanel(previousPanelIndex);
};
</script>

<template>
  <div class="c-carousel">
    <div class="c-carousel__controls" role="group" id="highlights-title">
      <h3 id="highlights-title" class="u-visually-hidden">Carousel controls</h3>
      <Button
        variant="carousel-control"
        alt-text="previous panel"
        @click="handlePreviousPanel"
        ><svg width="8.4" height="16.8" focusable="false">
          <use xlink:href="#icon-angle-left" /></svg
      ></Button>
      <Button
        variant="carousel-control"
        alt-text="next panel"
        @click="handleNextPanel"
        ><svg width="8.4" height="16.8" focusable="false">
          <use xlink:href="#icon-angle-right" /></svg
      ></Button>
    </div>
    <Panel
      v-show="currentPanel === index"
      v-for="(item, index) in items"
      :key="item.title"
      v-bind="item"
    />
  </div>
</template>
<style scoped lang="scss">
@use "../scss/functions" as f;

.c-carousel {
  position: relative;

  &__controls {
    position: absolute;
    bottom: 0rem;
    right: 0rem;
  }
}
</style>
