<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const menuOpen = ref(false);
const activeSection = ref('home');

const navLinks = [
  { id: 'home', label: 'Home' },
  { id: 'education', label: 'Parcours scolaire' },
  { id: 'skills', label: 'Compétences' },
  { id: 'projects', label: 'Projets réalisés' },
  { id: 'contact', label: 'Contact' },
];

function toggleMenu() {
  menuOpen.value = !menuOpen.value;
}

function closeMenu() {
  menuOpen.value = false;
}

// Même logique de scroll-spy que ton script.js original, adaptée en Vue.
function onScroll() {
  const sections = document.querySelectorAll('section');
  const top = window.scrollY;

  sections.forEach((sec) => {
    const offset = sec.offsetTop - 150;
    const height = sec.offsetHeight;
    const id = sec.getAttribute('id');

    if (top >= offset && top < offset + height) {
      activeSection.value = id;
    }
  });
}

onMounted(() => window.addEventListener('scroll', onScroll));
onUnmounted(() => window.removeEventListener('scroll', onScroll));
</script>

<template>
  <header class="header">
    <a href="#home" class="logo">
      Mounia <span class="logo-color">Ouattara</span>
    </a>

    <i class="bx bx-menu" :class="{ 'bx-x': menuOpen }" @click="toggleMenu"></i>

    <nav class="navbar" :class="{ active: menuOpen }">
      <a
        v-for="link in navLinks"
        :key="link.id"
        :href="`#${link.id}`"
        :class="{ active: activeSection === link.id }"
        @click="closeMenu"
      >
        {{ link.label }}
      </a>
    </nav>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  padding: 4rem 12% 4rem;
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(10px);
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 100;
}
.logo {
  font-size: 3rem;
  font-weight: 800;
  color: var(--text-color);
  cursor: pointer;
  transition: 0.3s ease;
}
.logo:hover {
  transform: scale(1.1);
}
.logo-color {
  color: var(--main-color);
  text-shadow: 0 0 25px var(--main-color);
}
.navbar a {
  font-size: 1.8rem;
  color: var(--text-color);
  margin-left: 4rem;
  font-weight: 500;
  transition: 0.3s ease;
  border-bottom: 3px solid transparent;
}
.navbar a:hover,
.navbar a.active {
  color: var(--main-color);
  border-bottom: 3px solid var(--main-color);
}
.bx-menu {
  display: none;
  font-size: 3.6rem;
  color: var(--main-color);
  cursor: pointer;
}

@media (max-width: 895px) {
  .header {
    padding: 2rem 3%;
  }
  .bx-menu {
    display: block;
  }
  .navbar {
    position: absolute;
    top: 100%;
    right: 0;
    width: 50%;
    padding: 1rem 3%;
    background: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(20px);
    border-bottom-left-radius: 2rem;
    border-left: 2px solid var(--main-color);
    border-bottom: 2px solid var(--main-color);
    display: none;
  }
  .navbar.active {
    display: block;
  }
  .navbar a {
    display: block;
    font-size: 2rem;
    margin: 3rem 0;
    color: white;
  }
}

@media (max-width: 600px) {
  .logo {
    font-size: 2.2rem;
  }
  .navbar {
    width: 70%;
  }
}

@media (max-width: 380px) {
  .header {
    padding: 1.5rem 4%;
    height: 64px;
  }
  .logo {
    font-size: 1.8rem;
  }
  .bx-menu {
    font-size: 2.8rem;
  }
  .navbar {
    width: 85%;
  }
  .navbar a {
    font-size: 1.7rem;
    margin: 2rem 0;
  }
}
</style>