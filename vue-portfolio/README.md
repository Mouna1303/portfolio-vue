# Portfolio — Mounia Ouattara (Vue 3)

Conversion de ton portfolio HTML/CSS/JS vers Vue 3 + Vite, en gardant exactement
le même thème visuel (fond `#080808`, accent crimson `#6f0431`).

## Installation

```bash
npm install
npm run dev
```

Puis ouvre l'URL affichée dans le terminal (en général `http://localhost:5173`).

Pour générer la version de production :

```bash
npm run build
```

## Structure

```
src/
  components/
    BgLogos.vue          — logos flottants en arrière-plan
    AppHeader.vue         — nav + scroll-spy + menu mobile
    HeroSection.vue        — accueil, photo, anneau de code, animation machine à écrire
    EducationTimeline.vue  — parcours scolaire
    SkillsSection.vue      — grille de compétences
    ProjectsSection.vue    — projets réalisés
    ContactSection.vue     — formulaire de contact
    AppFooter.vue          — footer
  data/
    education.js, skills.js, projects.js   — contenu séparé de l'affichage
```

## Erreurs corrigées par rapport à l'original

1. **`style.css` contenait deux feuilles de style superposées** — ton fichier
   mélangeait ta vraie CSS avec celle d'une ancienne version générée du
   portfolio (classes `.hero`, `.proj-card`, `.tl-item`, `.about`, `.stat`...
   jamais utilisées dans ton HTML, ~380 lignes mortes). Tout a été nettoyé :
   chaque composant Vue n'a que le CSS qu'il utilise réellement.
2. **Titre "Compétences" affiché deux fois** dans la section skills (un
   `<h2 class="heading">` ET un `.section-title` juste en dessous). Un seul
   gardé.
3. **`animation: animate 1s linear infinite`** sur `.text-animation span`
   référençait une `@keyframes animate` qui n'existait nulle part dans le
   fichier — règle invalide, supprimée (l'animation visible vient de
   `::before`/`::after`, qui fonctionnait déjà correctement).
4. **Lien CV cassé** : `href="img1.jpeg" download="CV_Mounia_Ouattara.pdf"`
   téléchargeait ta photo de profil en la faisant passer pour un PDF (fichier
   illisible à l'ouverture). Le bouton pointe maintenant vers `/cv.pdf`.
5. **Images de projets cassées** : `images/agrilink.png` et `src="Yowl"`
   n'existaient pas dans ton dossier → icône d'image cassée à l'affichage.
   Remplacées par un placeholder propre (initiale du projet) en attendant tes
   vraies captures d'écran.
6. **Lien "Démo" vide** pour AgriLink (`href=""`) → affiche maintenant
   "Démo bientôt disponible" au lieu d'un lien mort.
7. **Lien footer cassé** : "Projets réalisés" pointait vers `#projects` alors
   que la section s'appelait `id="testimonials"`. Tous les ids/ancres sont
   maintenant cohérents (`#home`, `#education`, `#skills`, `#projects`,
   `#contact`).
8. **`<html lang="en">`** alors que tout le contenu est en français → `lang="fr"`.
9. **2 fausses cartes "John Doe / lorem ipsum"** dans la section projets,
   restées en placeholder → supprimées (il ne reste que AgriLink et YOWL).
10. **Entrée du parcours scolaire dupliquée** : tu avais deux fois "WeCode —
    2026" à l'identique. J'ai remplacé la seconde par "Epitech Coding Academy"
    (mentionné comme une de tes formations) — à corriger si ce n'est pas ce
    que tu voulais.

## Reste à faire de ton côté (contenu, pas du code)

- [ ] Ajouter ton vrai CV dans `public/cv.pdf`
- [ ] Ajouter l'URL de démo réelle d'AgriLink dans `src/data/projects.js`
      (`demoUrl: '...'`) — l'aperçu se générera automatiquement dès que le lien existe
- [ ] Compléter la vraie description du projet YOWL
- [ ] Brancher un vrai envoi du formulaire de contact (Formspree, EmailJS, ou
      ton propre backend NestJS) — pour l'instant il affiche juste un message
      de confirmation côté client, sans rien envoyer
- [ ] Mettre tes vrais liens GitHub/Twitter/Instagram/LinkedIn (actuellement `#`)

## Aperçus de projets en direct (au lieu de captures d'écran)

`ProjectsSection.vue` génère automatiquement un aperçu visuel de chaque projet
à partir de son `demoUrl`, via le service gratuit
[microlink.io](https://microlink.io) — pas besoin de prendre des screenshots
à la main.

```js
function previewSrc(url) {
  return `https://api.microlink.io/?url=${encodeURIComponent(url)}&screenshot=true&meta=false&embed=screenshot.url`;
}
```

Priorité d'affichage pour chaque carte projet :
1. `project.image` si tu en fournis une (ajout manuel)
2. sinon, capture live générée depuis `project.demoUrl`
3. sinon (pas de lien, ou capture qui échoue), placeholder avec l'initiale du projet

**Limites à connaître** : le niveau gratuit de microlink.io est limité en
nombre de requêtes par jour (suffisant pour un portfolio perso à faible
trafic) et certains sites bloquent ce type de capture (en-têtes
`X-Frame-Options` / anti-bot). Si ça arrive, la carte retombe automatiquement
sur le placeholder. Pour un usage plus intensif, crée un compte gratuit sur
microlink.io et ajoute ta clé API dans l'URL (`&apiKey=...`).

