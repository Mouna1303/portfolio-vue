<script setup>
import { reactive, ref, computed, watch } from 'vue';
import { projects } from '../data/projects.js';

// Échecs de chargement d'aperçu (site qui refuse d'être capturé, service hors ligne, etc.)
const previewFailed = reactive({});

// Génère une capture d'écran live du site à partir de son URL, via microlink.io
// (gratuit, sans clé API pour un usage léger — s'applique à N'IMPORTE QUEL projet
// qui a un demoUrl rempli dans data/projects.js, pas seulement YOWL).
function previewSrc(url) {
  return `https://api.microlink.io/?url=${encodeURIComponent(url)}&screenshot=true&meta=false&embed=screenshot.url`;
}

// ----- Pagination -----
const itemsPerPage = 4;
const currentPage = ref(1);

const totalPages = computed(() => Math.max(1, Math.ceil(projects.length / itemsPerPage)));

const paginatedProjects = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return projects.slice(start, start + itemsPerPage);
});

function goToPage(page) {
  currentPage.value = page;
}
function prevPage() {
  if (currentPage.value > 1) currentPage.value--;
}
function nextPage() {
  if (currentPage.value < totalPages.value) currentPage.value++;
}
</script>

<template>
  <section class="projects" id="projects">
    <h2 class="heading">Projets réalisés</h2>

    <div class="wrapper">
      <div class="project-card" v-for="project in paginatedProjects" :key="project.title">
        <!-- 1. Image fournie à la main (si tu en ajoutes une un jour) -->
        <div class="project-thumb" v-if="project.image">
          <img :src="project.image" :alt="project.title" />
        </div>

        <!-- 2. Sinon, aperçu live généré depuis le lien de démo -->
        <div
          class="project-thumb"
          v-else-if="project.demoUrl && !previewFailed[project.title]"
        >
          <img
            :src="previewSrc(project.demoUrl)"
            :alt="`Aperçu en direct de ${project.title}`"
            loading="lazy"
            @error="previewFailed[project.title] = true"
          />
        </div>

        <!-- 3. Sinon (pas d'image, pas de lien, ou capture échouée) : placeholder -->
        <div class="project-thumb placeholder" v-else>
          {{ project.title.charAt(0) }}
        </div>

        <div class="project-body">
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>

          <a v-if="project.demoUrl" :href="project.demoUrl" target="_blank" rel="noopener" class="btn">
            Démo
          </a>
          <span v-else class="btn btn-disabled">Démo bientôt disponible</span>
        </div>
      </div>
    </div>

    <div class="pagination" v-if="totalPages > 1">
      <button class="page-arrow" :disabled="currentPage === 1" @click="prevPage">
        <i class="bx bx-chevron-left"></i>
      </button>

      <button
        v-for="page in totalPages"
        :key="page"
        class="page-dot"
        :class="{ active: page === currentPage }"
        @click="goToPage(page)"
      >
        {{ page }}
      </button>

      <button class="page-arrow" :disabled="currentPage === totalPages" @click="nextPage">
        <i class="bx bx-chevron-right"></i>
      </button>
    </div>
  </section>
</template>

<style scoped>
.projects {
  background: var(--secondary-bg-color);
}
.wrapper {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 3rem;
  max-width: 1000px;
  margin: 0 auto;
}
.project-card {
  background: rgba(0, 0, 0, 0.7);
  border: 3px solid rgba(238, 238, 238, 0.2);
  border-radius: 2rem;
  overflow: hidden;
  cursor: pointer;
  transition: 0.3s ease-in-out;
  color: white;
}
.project-card:hover {
  border: 3px solid var(--main-color);
  transform: translateY(-10px) scale(1.03);
  box-shadow: 0 0 50px var(--main-color);
}

/* Aperçu façon capture de navigateur : rectangulaire, pas circulaire. */
.project-thumb {
  width: 100%;
  aspect-ratio: 16 / 10;
  background: var(--bg-color);
  border-bottom: 3px solid var(--main-color);
  overflow: hidden;
}
.project-thumb img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top;
}
.project-thumb.placeholder {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 5rem;
  font-weight: 800;
  color: var(--main-color);
}

.project-body {
  padding: 2.5rem 3rem 3rem;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
  gap: 1.2rem;
}
.project-card h3 {
  font-size: 2.4rem;
}
.project-card p {
  font-size: 1.4rem;
  line-height: 1.6;
}
.btn-disabled {
  opacity: 0.5;
  cursor: not-allowed;
  box-shadow: none;
}

/* ----- Pagination ----- */
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin-top: 4rem;
}
.page-arrow,
.page-dot {
  background: transparent;
  border: 2px solid var(--main-color);
  color: var(--text-color);
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  font-size: 1.6rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 0.3s ease-in-out;
}
.page-arrow:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}
.page-dot.active {
  background: var(--main-color);
  box-shadow: 0 0 15px var(--main-color);
  font-weight: 700;
}
.page-arrow:not(:disabled):hover,
.page-dot:not(.active):hover {
  border-color: var(--text-color);
  transform: scale(1.1);
}

@media (max-width: 991px) {
  .wrapper {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .project-body {
    padding: 1.8rem 1.8rem 2.2rem;
  }
  .project-card h3 {
    font-size: 2rem;
  }
  .project-card p {
    font-size: 1.3rem;
  }
  .page-arrow,
  .page-dot {
    width: 3.4rem;
    height: 3.4rem;
    font-size: 1.4rem;
  }
}
</style>