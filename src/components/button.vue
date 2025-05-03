<script setup lang="ts">
import { useTemplateRef } from "vue";

const {
  variant,
  altText = null,
  expanded = null,
} = defineProps<{
  variant: "normal" | "carousel-control" | "menu-control";
  altText: string | null;
  expanded: boolean | null;
}>();

const emit = defineEmits(["click"]);

const btn = useTemplateRef<HTMLButtonElement>("btn");

const focusBtn = () => {
  btn.value?.focus();
};

defineExpose({
  focusBtn,
});
</script>
<template>
  <button
    v-if="expanded !== null"
    class="c-button | u-text-button u-fw-500 u-fc-black"
    :data-variant="variant"
    @click="emit('click')"
    ref="btn"
    :aria-expanded="expanded"
  >
    <slot></slot>
    <span v-if="altText !== undefined" class="u-visually-hidden">
      ({{ altText }})</span
    >
  </button>
  <button
    v-else
    class="c-button | u-text-button u-fw-500 u-fc-black"
    :data-variant="variant"
    @click="emit('click')"
    ref="btn"
  >
    <slot></slot>
    <span v-if="altText !== null" class="u-visually-hidden">
      ({{ altText }})</span
    >
  </button>
</template>
<style lang="scss">
@use "../scss/functions" as f;

.c-button {
  cursor: pointer;
  border: none;
  display: inline-flex;
  justify-content: center;
  align-items: center;

  &:focus {
    outline: 0.4rem dashed var(--very-dark-gray);
  }

  &[data-variant="normal"] {
    background-color: transparent;
    gap: 3rem;

    &:hover {
      color: var(--dark-gray);

      & svg {
        color: var(--gray);
      }
    }
  }

  &[data-variant="carousel-control"] {
    background-color: var(--black);
    padding: 1.96rem 2.38rem;

    & svg {
      @include f.breakpoint(medium) {
        width: 1.2rem;
        height: 2.4rem;
      }
    }

    @include f.breakpoint(medium) {
      padding: 2.8rem 3.4rem;
    }

    &:hover {
      background-color: var(--very-dark-gray);
    }
  }

  &[data-variant="menu-control"] {
    background-color: transparent;
  }
}
</style>
