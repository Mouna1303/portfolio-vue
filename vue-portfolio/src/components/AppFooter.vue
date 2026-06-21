<script setup></script>

<template>
  <footer class="footer">
    <div class="social">
      <a href="https://github.com/Mouna1303" aria-label="GitHub"><i class="bx bxl-github"></i></a>
      <a href="#" aria-label="Twitter"><i class="bx bxl-twitter"></i></a>
      <a href="#" aria-label="Instagram"><i class="bx bxl-instagram"></i></a>
      <a href="https://www.linkedin.com/in/noura-ouattara-a2392b3b4/" aria-label="LinkedIn"><i class="bx bxl-linkedin"></i></a>
    </div>
    <ul class="list">
      <li><a href="#education">Parcours scolaire</a></li>
      <li><a href="#skills">Compétences</a></li>
      <!-- avant: href="#projects" alors que la section s'appelait "testimonials" -> lien mort -->
      <li><a href="#projects">Projets réalisés</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <p class="copyright">© Mounia Ouattara | All Rights Reserved</p>
  </footer>
</template>

<style scoped>
.footer {
  position: relative;
  width: 100%;
  padding: 40px 0;
  background-color: var(--secondary-bg-color);
}
.social {
  text-align: center;
  padding-bottom: 25px;
}
.social a {
  font-size: 25px;
  color: var(--main-color);
  border: 2px solid var(--main-color);
  width: 42px;
  height: 42px;
  line-height: 42px;
  display: inline-block;
  text-align: center;
  border-radius: 50%;
  margin: 0 10px;
  transition: 0.3s ease-in-out;
}
.social a:hover {
  transform: scale(1.2) translateY(-10px);
  background-color: var(--main-color);
}
.list {
  margin: 0;
  padding: 0;
  font-size: 18px;
  line-height: 1.6;
  text-align: center;
  list-style: none;
}
.list li a {
  color: white;
  border-bottom: 3px solid transparent;
  transition: 0.3s ease-in-out;
}
.list li a:hover {
  border-bottom: 3px solid var(--main-color);
}
.list li {
  display: inline-block;
  padding: 0 15px;
}
.copyright {
  margin-top: 50px;
  text-align: center;
  font-size: 16px;
  color: white;
}

@media (max-width: 991px) {
  .footer {
    padding: 2rem 3%;
  }
}
</style>
