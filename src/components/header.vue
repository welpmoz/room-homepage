<script setup lang="ts">
import { onUpdated, ref, useTemplateRef } from "vue";
import Button from "./button.vue";
import Dialog from "./dialog.vue";
import Navigation from "./navigation.vue";

type ButtonType = InstanceType<typeof Button>;

const showDialog = ref(false);
const openBtn = useTemplateRef<ButtonType>("openBtn");
const closeBtn = useTemplateRef<ButtonType>("closeBtn");

const toggleDialog = () => {
  showDialog.value = !showDialog.value;
};

onUpdated(() => {
  if (showDialog.value) {
    closeBtn.value?.focusBtn();
  } else {
    openBtn.value?.focusBtn();
  }
});
</script>

<template>
  <header class="c-header">
    <div class="l-header__wrapper">
      <div class="c-header__content" data-size="small">
        <div>
          <Button
            variant="menu-control"
            alt-text="open menu"
            @click="toggleDialog"
            ref="openBtn"
            :expanded="showDialog"
            ><svg width="20" height="14" focusable="false">
              <use xlink:href="#icon-hamburger" /></svg
          ></Button>
        </div>
        <div>
          <a href="#"
            ><svg width="62" height="14" focusable="false">
              <use xlink:href="#logo" />
            </svg>
          </a>
        </div>
        <div></div>
      </div>
      <div class="c-header__content" data-size="large">
        <a href="#"
          ><svg width="62" height="14" focusable="false">
            <use xlink:href="#logo" />
          </svg>
        </a>
        <Navigation
          :items="['home', 'shop', 'about', 'contact']"
          accent-color="white"
        />
      </div>
      <Dialog :show="showDialog"
        ><Button
          variant="menu-control"
          alt-text="close menu"
          @click="toggleDialog"
          ref="closeBtn"
          ><svg width="16" height="16" focusable="false">
            <use xlink:href="#icon-close" /></svg></Button
      ></Dialog>
    </div>
  </header>
</template>

<style scoped lang="scss">
@use "../scss/functions" as f;

.c-header {
  position: absolute;
  z-index: 5;
  width: 100%;
  padding-top: 4.8rem;

  @include f.breakpoint(large) {
    padding-top: 6.3rem;
  }

  &__content {
    &[data-size="small"] {
      display: flex;
      align-items: center;
      gap: 11.3rem;

      @include f.breakpoint(large) {
        display: none;
      }

      & div {
        flex-grow: 1;
      }
    }

    &[data-size="large"] {
      display: none;

      @include f.breakpoint(large) {
        display: flex;
        gap: 5.62rem;
      }
    }
  }
}

.l-header__wrapper {
  max-width: 32.7rem;
  margin: 0rem auto;

  @include f.breakpoint(medium) {
    max-width: 42rem;
  }

  @include f.breakpoint(large) {
    max-width: 131.2rem;
  }
}
</style>
