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

    <!-- <div class="home-img">
      <img :src="profileImg" alt="Photo de Mounia Ouattara" />
      <svg class="code-ring" viewBox="0 0 500 500">
        <defs>
          <path
            id="circle-path"
            d="M 250,250
               m -240,0
               a 240,240 0 1,1 480,0
               a 240,240 0 1,1 -480,0"
          />
        </defs>
        <text
          fill="#ffffff"
          style="fill: #ffffff !important"
          font-family="Courier New"
          font-size="18"
          font-weight="bold"
        >
          <textPath href="#circle-path" spacing="auto">
            &#160;print("Croit en toi") &#160;|&#160; if toi == forte:
            &#160;|&#160; &#160;succeed() &#160;|&#160; def
            croit_en_toi(): &#160;|&#160; &#160;return True &#160;|&#160;
            while reve: &#160;|&#160; &#160;avance() &#160;|&#160;
          </textPath>
        </text>
      </svg>
    </div> -->
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
  font-size: 7rem;
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
.code-ring {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 48vw;
  height: 40vw;
  animation: spinRing 20s linear infinite;
  pointer-events: none;
}
@keyframes spinRing {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}
.home-img img {
  position: relative;
  top: 3rem;
  width: 32vw;
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
  .home-content h3 {
    font-size: 2.6rem;
  }
  .home-content h1 {
    font-size: 8rem;
    margin-top: 3rem;
  }
  .home-content p {
    max-width: 600px;
    margin: 0 auto;
  }
  .home-img img {
    width: 56vw;
  }
}
</style>
