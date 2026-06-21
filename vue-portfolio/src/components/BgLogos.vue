<script setup>
const logos = [
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/php/php-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/flask/flask-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nestjs/nestjs-plain.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nextjs/nextjs-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-plain.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-plain.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg',
  'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg',
];

const TOTAL = 40;

// On génère les propriétés de chaque logo une seule fois (au chargement du composant),
// exactement comme le faisait ton script.js original.
const floatingLogos = Array.from({ length: TOTAL }, () => ({
  src: logos[Math.floor(Math.random() * logos.length)],
  left: Math.random() * 100 + 'vw',
  size: 30 + Math.random() * 40 + 'px',
  duration: 8 + Math.random() * 15 + 's',
  delay: Math.random() * 10 + 's',
}));
</script>

<template>
  <div class="bg-logos">
    <img
      v-for="(logo, index) in floatingLogos"
      :key="index"
      :src="logo.src"
      alt=""
      :style="{
        left: logo.left,
        width: logo.size,
        height: logo.size,
        animationDuration: logo.duration,
        animationDelay: logo.delay,
      }"
    />
  </div>
</template>

<style scoped>
.bg-logos {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  overflow: hidden;
  pointer-events: none;
}
.bg-logos img {
  position: absolute;
  object-fit: contain;
  opacity: 0.35;
  animation-name: floatUp;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}
@keyframes floatUp {
  0% {
    transform: translateY(100vh) rotate(0deg);
    opacity: 0;
  }
  10% {
    opacity: 0.07;
  }
  90% {
    opacity: 0.07;
  }
  100% {
    transform: translateY(-150px) rotate(360deg);
    opacity: 0;
  }
}
</style>
