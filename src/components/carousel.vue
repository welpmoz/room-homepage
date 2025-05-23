<script setup lang="ts">
import { onUpdated, ref, useTemplateRef } from "vue";
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
const alertsDiv = useTemplateRef<HTMLDivElement>("alertsDiv");
let alertInterval: number;

const pushAlertMessage = (message: string) => {
  if (alertsDiv.value) {
    const alert = document.createElement("div");
    alert.setAttribute("role", "alert");
    alert.innerHTML = message;
    alertsDiv.value.appendChild(alert);
    clearTimeout(alertInterval);
    alertInterval = setTimeout(() => {
      alertsDiv.value!.innerHTML = "";
    }, 2000);
  }
};

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

onUpdated(() => {
  pushAlertMessage(
    `Showing panel ${currentPanel.value + 1} of (${items.length})`
  );
});
</script>

<template>
  <section class="c-carousel" aria-labelledby="carousel-title">
    <h2 class="u-visually-hidden" id="carousel-title">
      Carousel furniture highlights
    </h2>
    <div
      class="c-carousel__controls"
      role="group"
      aria-labelledby="highlights-title"
    >
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
    <Transition mode="out-in">
      <Panel
        v-if="currentPanel === 0"
        :key="items[0].title"
        v-bind="items[0]"
      />
      <Panel
        v-else-if="currentPanel === 1"
        :key="items[1].title"
        v-bind="items[1]"
      />
      <Panel
        v-else-if="currentPanel === 2"
        :key="items[2].title"
        v-bind="items[2]"
      />
    </Transition>
    <div class="u-visually-hidden" ref="alertsDiv"></div>
  </section>
</template>
<style scoped lang="scss">
@use "../scss/functions" as f;

.v-enter-active,
.v-leave-active {
  transition: all 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  transform: translateX(-30px);
  opacity: 0;
}

.c-carousel {
  position: relative;

  &__controls {
    position: absolute;
    top: 30.4rem;
    right: 0rem;
    z-index: 5;

    @include f.breakpoint(medium) {
      top: 37rem;
    }

    @include f.breakpoint(large) {
      top: 45.4rem;
      right: unset;
      left: 84rem;
      transform: translateX(-100%);
    }
  }
}
</style>
