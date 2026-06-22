<script setup>
import profileImg from '../assets/img.png';
</script>

<template>
  <section class="home" id="home">
    <div class="home-content">
      <h1>Bonjour, je suis <span>Mounia Ouattara</span></h1>
      <h3 class="text-animation"><span></span></h3>
      <p>
        Développeuse Web & Mobile passionnée par la création d'applications
        modernes, performantes et intuitives. Je travaille avec certains
        langages de programmation pour développer des solutions adaptées aux
        besoins des utilisateurs.
      </p>

      <div class="social-icons">
        <a href="#" aria-label="GitHub"><i class="bx bxl-github"></i></a>
        <a href="#" aria-label="Twitter"><i class="bx bxl-twitter"></i></a>
        <a href="#" aria-label="Instagram"><i class="bx bxl-instagram"></i></a>
        <a href="#" aria-label="LinkedIn"><i class="bx bxl-linkedin"></i></a>
      </div>

      <div class="btn-group">
        <!--
          ⚠️ Mounia : avant le href pointait vers img1.jpeg avec download="...pdf" —
          ça téléchargeait ta photo en la faisant passer pour un PDF (fichier corrompu
          à l'ouverture). Mets ton vrai CV dans public/cv.pdf pour que ce lien marche.
        -->
        <a href="/cv.pdf" download="CV_Mounia_Ouattara.pdf" class="btn">Download CV</a>
        <a href="#projects" class="btn">Voir mes projets</a>
        <a href="#contact" class="btn">Contact</a>
      </div>
    </div>

    <div class="home-img">
  <img :src="profileImg" alt="Photo de Mounia Ouattara" />
</div>
  </section>
</template>

<style scoped>
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15rem;
}
.home-content {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  text-align: left;
  justify-content: center;
  margin-top: 3rem;
}
.home-content span {
  color: var(--main-color);
}
.home-content h3 {
  margin-bottom: 2rem;
  margin-top: 1rem;
  font-size: 3.5rem;
}
.home-content h1 {
  font-size: 4rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  line-height: 1;
}
.home-content p {
  font-size: 1.5rem;
  font-weight: 500;
  line-height: 1.8;
  max-width: 1000px;
}
.home-img {
  position: relative;
  overflow: visible;
}



.home-img img {
  position: relative;
  top: 3rem;
  width: 32vw;
  height: 32vw;
  object-fit: cover;
  border-radius: 50%;
  box-shadow: 0 0 25px var(--main-color);
  cursor: pointer;
  transition: 0.4s ease-in-out;
}
.home-img img:hover {
  box-shadow:
    0 0 25px var(--main-color),
    0 0 50px var(--main-color),
    0 0 100px var(--main-color);
}
.social-icons a {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  width: 4.5rem;
  height: 4.5rem;
  background: transparent;
  border: 2px solid var(--main-color);
  font-size: 2.5rem;
  border-radius: 50%;
  color: var(--main-color);
  margin: 3rem 1.5rem 3rem 0;
  transition: 0.3s ease-in-out;
}
.social-icons a:hover {
  color: var(--text-color);
  transform: scale(1.3) translate(-5px);
  box-shadow: 0 0 25px var(--main-color);
  background: var(--main-color);
}
.btn {
  display: inline-block;
  padding: 1rem 2.5rem;
  background: var(--main-color);
  box-shadow: 0 0 25px var(--main-color);
  border-radius: 4rem;
  font-size: 1.5rem;
  color: black;
  border: 2px solid transparent;
  letter-spacing: 0.1rem;
  font-weight: 600;
  transition: 0.3s ease-in-out;
  cursor: pointer;
}
.btn:hover {
  transform: scale(1.05);
  box-shadow: 0 0 50px var(--main-color);
}
.btn-group {
  display: flex;
  gap: 1.5rem;
  align-items: center;
}
.btn-group a:nth-of-type(2) {
  background-color: black;
  color: var(--main-color);
  border: 2px solid var(--main-color);
}
.btn-group a:nth-of-type(2):hover {
  background-color: var(--main-color);
  color: black;
  box-shadow: 0 0 25px var(--main-color);
}

/* Animation "machine à écrire" en pur CSS (content animé sur ::before) */
.text-animation {
  font-size: 34px;
  font-weight: 600;
  min-width: 280px;
  position: relative;
  display: inline-flex;
}
.text-animation span {
  top: 0;
  left: 0;
  color: var(--main-color);
  animation: animate 1s linear infinite;
  position: relative;
  margin-left: 10px;
}
.text-animation span::before {
  content: 'web & mobile woman developer';
  color: var(--main-color);
  animation: words 20s infinite;
}
.text-animation span::after {
  content: '';
  background-color: var(--main-color);
  position: absolute;
  width: calc(100% + 8px);
  height: 100%;
  border-left: 3px solid var(--bg-color);
  right: -8px;
  animation:
    cursor 0.6s infinite,
    typing 20s steps(14) infinite;
}
@keyframes cursor {
  to {
    border-left: 2px solid var(--main-color);
  }
}
@keyframes words {
  0%,
  20% {
    content: 'Front-end & back-end developer';
  }
  21%,
  40% {
    content: 'web & mobile developer';
  }
  41%,
  60% {
    content: 'dev junior';
  }
  61%,
  80% {
    content: 'web & mobile woman developer';
  }
  81%,
  100% {
    content: 'Front-end & back-end developer';
  }
}
@keyframes typing {
  10%,
  15%,
  30%,
  35%,
  50%,
  55%,
  70%,
  75%,
  90%,
  95% {
    width: 0;
  }
  5%,
  20%,
  25%,
  40%,
  45%,
  60%,
  65%,
  80%,
  85% {
    width: calc(100% + 8px);
  }
}

@media (max-width: 895px) {
  .home {
    flex-direction: column-reverse;
    margin: 5rem 4rem;
  }
  .home-content {
    align-items: center;
    text-align: center;
  }
  .home-content h3 {
    font-size: 2.6rem;
  }
  .home-content h1 {
    font-size: 5.5rem;
    margin-top: 3rem;
  }
  .home-content p {
    max-width: 600px;
    margin: 0 auto;
  }
  .home-img img {
    width: 56vw;
    height: 56vw;
  }
  .btn-group {
    flex-wrap: wrap;
    justify-content: center;
  }
}

@media (max-width: 600px) {
  .home {
    margin: 4rem 2rem;
    gap: 3rem;
  }
  .home-content h1 {
    font-size: 4rem;
  }
  .home-content h3 {
    font-size: 2rem;
  }
  .home-content p {
    font-size: 1.3rem;
    max-width: 100%;
  }
  .home-img img {
    width: 65vw;
    height: 65vw;
  }
  .social-icons a {
    width: 3.8rem;
    height: 3.8rem;
    font-size: 2rem;
    margin: 2rem 1rem 2rem 0;
  }
  .btn {
    padding: 0.9rem 1.8rem;
    font-size: 1.3rem;
  }
}

@media (max-width: 380px) {
  .home {
    margin: 3rem 1.2rem;
  }
  .home-content h1 {
    font-size: 3.2rem;
  }
  .home-content h3 {
    font-size: 1.7rem;
  }
  .text-animation {
    min-width: 0;
    font-size: 1.7rem;
  }
  .home-img img {
    width: 72vw;
    height: 72vw;
  }
  .btn-group {
    flex-direction: column;
    width: 100%;
  }
  .btn {
    width: 100%;
    text-align: center;
  }
}
</style>