<script setup lang="ts">
import { onBeforeUnmount, onUpdated, useTemplateRef } from "vue";
import Navigation from "./navigation.vue";

const { show } = defineProps<{
  show: boolean;
}>();

const dialogRef = useTemplateRef<HTMLElement>("dialogRef");

function trapFocus(e: KeyboardEvent) {
  if (!dialogRef.value) return;
  const focusable = dialogRef.value.querySelectorAll<HTMLElement>(
    'a[href], button:not([disabled]), textarea, input, select, [tabindex]:not([tabindex="-1"])'
  );
  if (!focusable.length) return;

  const first = focusable[0];
  const last = focusable[focusable.length - 1];

  if (e.key === "Tab") {
    if (e.shiftKey) {
      if (document.activeElement === first) {
        e.preventDefault();
        last.focus();
      }
    } else {
      if (document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
  }
}

onUpdated(() => {
  if (show) {
    document.addEventListener("keydown", trapFocus);
  } else {
    document.removeEventListener("keydown", trapFocus);
  }
});

onBeforeUnmount(() => {
  document.removeEventListener("keydown", trapFocus);
});
</script>

<template>
  <div role="dialog" aria-modal>
    <div role="document">
      <div v-if="show" class="c-dialog__curtain"></div>
      <div class="c-dialog" :hidden="!show" ref="dialogRef">
        <div class="l-dialog__wrapper">
          <div class="c-dialog__body">
            <slot></slot>
            <Navigation
              :items="['home', 'shop', 'about', 'contact']"
              accent-color="black"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
@use "../scss/functions" as f;

.c-dialog {
  position: fixed;
  z-index: 15;
  top: 0rem;
  left: 0rem;
  width: 100%;
  background-color: var(--white);

  @include f.breakpoint(large) {
    display: none;
  }

  &__body {
    display: flex;
    align-items: flex-start;
    gap: 6.6rem;
    padding: 4.7rem 0rem 3.9rem 0rem;
  }

  &__curtain {
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    background-color: var(--black);
    opacity: 0.5;
    z-index: 5;

    @include f.breakpoint(large) {
      display: none;
    }
  }
}

.l-dialog {
  &__wrapper {
    max-width: 32.6rem;
    margin: 0rem auto;
  }
}
</style>
