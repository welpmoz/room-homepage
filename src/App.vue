<script setup lang="ts">
import About from "./components/about.vue";
import Carousel from "./components/carousel.vue";
import Header from "./components/header.vue";
import SVGDefinitions from "./components/svg-definitions.vue";

const furnitureHighlights = [
  {
    title: "Discover innovative ways to decorate",
    description: `We provide unmatched quality,
        comfort, and style for property owners across the country. Our experts
        combine form and function in bringing your vision to life. Create a room
        in your own style with our collection and make your property a
        reflection of you and what you love.`,
    imgName: "hero-1",
    altImg: `Sillas blancas de diseño moderno alrededor de una mesa de madera clara con patas blancas, sobre la mesa hay un bonsái en una maceta negra, fondo de pared gris claro.`,
  },
  {
    title: "We are available all across the globe",
    description: `With stores all over the world, it's easy for you to find furniture for your home or place of business. Locally, we’re in most major cities throughout the country. Find the branch nearest you using our store locator. Any questions? Don't hesitate to contact us today.`,
    imgName: "hero-2",
    altImg: `Tres sillas de colores pastel, una amarilla, una verde claro y una blanca, con diseño minimalista y patas delgadas, sobre un fondo de pared gris.`,
  },
  {
    title: "Manufactured with the best materials",
    description: `Our modern furniture store provide a high level of quality. Our company has invested in advanced technology to ensure that every product is made as perfect and as consistent as possible. With three decades of experience in this industry, we understand what customers want for their home and office.`,
    imgName: "hero-3",
    altImg: `Silla plegable negra de metal y asiento acolchado, fotografiada de perfil sobre un fondo oscuro.`,
  },
];
</script>
<template>
  <Header />
  <main>
    <SVGDefinitions />

    <Carousel :items="furnitureHighlights" />

    <About />

    <div class="attribution">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
        >Frontend Mentor</a
      >. Coded by <a href="#">Your Name Here</a>.
    </div>
  </main>
</template>
