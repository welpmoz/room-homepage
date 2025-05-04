<script setup lang="ts">
import aboutLightImg from "../images/image-about-light.jpg";
import aboutDarkImg from "../images/image-about-dark.jpg";
</script>
<template>
  <section class="c-about">
    <img
      :src="aboutDarkImg"
      width="100%"
      height="266"
      alt="Sala moderna con dos sillones negros de estructura metálica y una mesa baja de madera clara con un cuenco blanco en el centro; al fondo, una cama y muebles en tonos oscuros, ambiente tenue y elegante."
      class="c-about__hero"
    />
    <div class="c-about__body">
      <h3 class="u-text-heading-2 u-fw-700 u-fc-black">About our furniture</h3>
      <p class="u-text-body u-fw-500 u-fc-dark-gray">
        Our multifunctional collection blends design and function to suit your
        individual taste. Make each room unique, or pick a cohesive theme that
        best express your interests and what inspires you. Find the furniture
        pieces you need, from traditional to contemporary styles or anything in
        between. Product specialists are available to help you create your dream
        space.
      </p>
    </div>
    <img
      :src="aboutLightImg"
      width="100%"
      height="266"
      alt="Silla blanca de diseño minimalista, completamente iluminada sobre un fondo blanco, resaltando sus líneas limpias y modernas."
      class="c-about__hero"
    />
  </section>
</template>
<style scoped lang="scss">
@use "../scss/functions" as f;

.c-about {
  @include f.breakpoint(large) {
    display: grid;
    grid-template-columns: 1fr 58rem 1fr;
  }

  &__hero {
    object-fit: cover;
    object-position: bottom center;
  }

  &__body {
    max-width: 31.1rem;
    margin: 0 auto;
    padding-top: 4.9rem;
    padding-bottom: 4.1rem;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;

    @include f.breakpoint(medium) {
      max-width: 36rem;
      padding-top: 5.5rem;
      padding-bottom: 4.7rem;
    }

    @include f.breakpoint(large) {
      max-width: 48.4rem;
      padding-top: 6.1rem;
      padding-bottom: 0rem;
    }
  }
}
</style>
