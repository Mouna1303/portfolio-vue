<script setup>
import BgLogos from './components/BgLogos.vue';
import AppHeader from './components/AppHeader.vue';
import HeroSection from './components/HeroSection.vue';
import EducationTimeline from './components/EducationTimeline.vue';
import SkillsSection from './components/SkillsSection.vue';
import ProjectsSection from './components/ProjectsSection.vue';
import ContactSection from './components/ContactSection.vue';
import AppFooter from './components/AppFooter.vue';
</script>

<template>
  <BgLogos />
  <AppHeader />
  <main>
    <HeroSection />
    <EducationTimeline />
    <SkillsSection />
    <ProjectsSection />
    <ContactSection />
  </main>
  <AppFooter />
</template>
