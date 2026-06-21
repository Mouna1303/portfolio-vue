<script setup>
import { skills } from '../data/skills.js';
</script>

<template>
  <section class="skills" id="skills">
    <div class="section-title">Mes <span>Compétences</span></div>
    <div class="divider"><span></span></div>
    <p class="section-sub">Technologies et outils que je maîtrise</p>

    <div class="skills-grid">
      <div class="skill-card" v-for="skill in skills" :key="skill.name">
        <div class="skill-icon">
          <img :src="skill.icon" :alt="skill.name" :style="skill.invert ? 'filter:invert(1)' : ''" />
        </div>
        <div>
          <div class="skill-name">{{ skill.name }}</div>
          <p class="skill-desc">{{ skill.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills {
  background: var(--bg-color);
}
.section-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(3.5rem, 4.5vw, 5.5rem);
  font-weight: 900;
  text-align: center;
  margin-bottom: 1.2rem;
}
.section-title span {
  color: var(--accent);
}
.section-sub {
  text-align: center;
  color: var(--muted);
  font-size: 1.5rem;
  margin-bottom: 6rem;
}
.divider {
  display: flex;
  justify-content: center;
  margin-bottom: 1.5rem;
}
.divider span {
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, var(--accent), var(--accent2));
  border-radius: 2px;
  display: block;
}
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2.5rem;
  max-width: 1000px;
  margin: 0 auto;
}
.skill-card {
  background: var(--bg3);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 3rem 2.5rem;
  display: flex;
  align-items: center;
  gap: 2rem;
  transition: all 0.35s;
  cursor: default;
}
.skill-card:hover {
  border-color: var(--accent);
  transform: translateY(-8px);
  box-shadow: var(--glow);
}
.skill-icon {
  width: 54px;
  height: 54px;
  border-radius: 14px;
  background: rgba(200, 68, 90, 0.1);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  overflow: hidden;
}
.skill-icon img {
  width: 34px;
  height: 34px;
  object-fit: contain;
}
.skill-name {
  font-family: 'Playfair Display', serif;
  font-size: 1.9rem;
  font-weight: 700;
  margin-bottom: 0.3rem;
  text-transform: capitalize;
  color: var(--text-color);
}
.skill-desc {
  color: var(--muted);
  font-size: 1.3rem;
  line-height: 1.5;
}

@media (max-width: 992px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 640px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>
