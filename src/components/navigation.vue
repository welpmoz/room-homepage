<script setup lang="ts">
const { items } = defineProps<{
  items: string[];
  accentColor: "black" | "white";
}>();
</script>
<template>
  <nav class="c-navigation">
    <ul
      class="c-navigation__list | u-text-link u-fw-600"
      :class="`u-fc-${accentColor}`"
    >
      <li v-for="item in items" class="c-navigation__item">
        <a href="#">{{ item }}</a>
        <hr :style="{ borderColor: `var(--${accentColor})` }" />
      </li>
    </ul>
  </nav>
</template>
<style scoped lang="scss">
.c-navigation {
  &__list {
    display: flex;
    gap: 3.1rem;
  }

  &__item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.8rem;

    & hr {
      opacity: 0;
      width: 1.6rem;
      border: 0.1rem solid;
      transition: opacity 300ms ease-in-out;
    }

    & a:hover {
      & ~ hr {
        opacity: 1;
      }
    }

    & a:focus {
      outline: 0.4rem dashed var(--very-dark-gray);
    }
  }
}
</style>
