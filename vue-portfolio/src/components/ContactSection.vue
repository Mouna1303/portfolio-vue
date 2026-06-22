<script setup>
import { ref } from 'vue';

// On crée un objet réactif pour récupérer les saisies du formulaire
const form = ref({
  name: '',
  email: '',
  phone: '',
  subject: '',
  message: ''
});

const sent = ref(false);

function handleSubmit() {
  // ⚠️ Remplace par TON adresse email réelle
  const monEmail = "ton.adresse.email@example.com"; 
  
  // On prépare le sujet du mail
  const sujetEmail = form.value.subject ? form.value.subject : `Contact Portfolio de ${form.value.name}`;
  
  // On construit le corps du message avec toutes les infos du formulaire
  const corpsEmail = `Nom : ${form.value.name}\n` +
                     `Email de contact : ${form.value.email}\n` +
                     `Téléphone : ${form.value.phone || 'Non renseigné'}\n\n` +
                     `Message :\n${form.value.message}`;

  // On encode les textes pour qu'ils soient compatibles avec une URL
  const sujetEncode = encodeURIComponent(sujetEmail);
  const corpsEncode = encodeURIComponent(corpsEmail);
  
  // Déclenche l'ouverture du logiciel de messagerie de l'utilisateur
  window.location.href = `mailto:${monEmail}?subject=${sujetEncode}&body=${corpsEncode}`;
  
  // Affiche le petit message de confirmation sous le bouton
  sent.value = true;
}
</script>

<template>
  <section class="contact" id="contact">
    <h2 class="heading">Contactez- <span>moi</span></h2>

    <form @submit.prevent="handleSubmit">
      <div class="input-box">
        <input type="text" v-model="form.name" placeholder="Votre nom" required />
        <input type="email" v-model="form.email" placeholder="Votre email" required />
      </div>
      <div class="input-box">
        <input type="tel" v-model="form.phone" placeholder="Numéro de téléphone" />
        <input type="text" v-model="form.subject" placeholder="Sujet" />
      </div>
      <textarea v-model="form.message" placeholder="Votre message" required></textarea>
      <button type="submit" class="btn">Envoyer</button>

      <p v-if="sent" class="confirmation">
        Votre application de messagerie vient de s'ouvrir pour envoyer le mail !
      </p>
    </form>
  </section>
</template>

<style scoped>
.contact {
  background-color: var(--bg-color);
}
.contact .heading {
  margin-bottom: 3rem;
  color: white;
}
.contact .heading span {
  color: var(--main-color);
}
form {
  max-width: 600px;
  margin: 5rem auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  text-align: center;
}
.input-box {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 100%;
}
.input-box input,
form textarea {
  width: 100%;
  padding: 2rem;
  font-size: 1.6rem;
  color: var(--text-color);
  background: var(--secondary-bg-color);
  border-radius: 2rem;
  border: 2px solid var(--main-color);
  margin: 0.7rem 0;
  resize: none;
}
form textarea {
  min-height: 150px;
}
.contact .btn {
  margin-top: 1rem;
}
.confirmation {
  color: var(--main-color);
  font-weight: 600;
  font-size: 1.4rem;
}

@media (max-width: 991px) {
  form {
    flex-direction: column;
  }
  .contact .heading {
    font-size: 3.5rem; /* Ajustez la valeur selon vos besoins */
    margin-bottom: 2rem;
  }
}

@media (max-width: 480px) {
  form {
    margin: 3rem auto;
  }
  .input-box input,
  form textarea {
    padding: 1.4rem;
    font-size: 1.4rem;
  }
  .contact .heading {
    font-size: 2.8rem; /* Plus petit pour les mobiles */
    margin-bottom: 1.5rem;
  }
}
</style>