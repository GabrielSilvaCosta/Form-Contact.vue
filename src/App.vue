<template>
  <div class="container">
    <h1 class="title">Contact Us</h1>

    <form @submit.prevent="handleSubmit">
      <div class="form-row">
        <div class="form-group">
          <label for="firstName">First Name *</label>
          <input
            type="text"
            id="firstName"
            name="firstName"
            v-model="firstName"
            required
            aria-label="Primeiro nome"
          />
          <span class="error" v-if="firstNameErrors">{{
            firstNameErrors
          }}</span>
        </div>
        <div class="form-group">
          <label for="lastName">Last Name *</label>
          <input
            type="text"
            id="lastName"
            name="lastName"
            v-model="lastName"
            required
            aria-label="Sobrenome"
          />
          <span class="error" v-if="lastNameErrors">{{ lastNameErrors }}</span>
        </div>
      </div>

      <div class="form-group">
        <label for="email">Email Address *</label>
        <input
          type="email"
          id="email"
          name="email"
          v-model="email"
          required
          aria-label="E-mail"
        />
        <span class="error" v-if="emailErrors">{{ emailErrors }}</span>
      </div>

      <div class="form-group">
        <label>Query Type *</label>
        <div class="radio-group">
          <label for="generalEnquiry">
            <input
              type="radio"
              id="generalEnquiry"
              name="queryType"
              value="generalEnquiry"
              v-model="queryType"
              required
            />
            General Enquiry
          </label>
          <label for="supportRequest">
            <input
              type="radio"
              id="supportRequest"
              name="queryType"
              value="supportRequest"
              v-model="queryType"
              required
            />
            Support Request
          </label>
        </div>
      </div>

      <div class="form-group">
        <label for="message">Message *</label>
        <textarea
          id="message"
          name="message"
          v-model="message"
          required
          aria-label="Mensagem"
        ></textarea>
        <span class="error" v-if="messageErrors">{{ messageErrors }}</span>
      </div>

      <div class="form-group checkbox-group">
        <input
          type="checkbox"
          id="consent"
          name="consent"
          v-model="consent"
          required
          aria-label="Consentimento para contato"
        />
        <label for="consent">I consent to being contacted by the team *</label>
      </div>

      <button type="submit" aria-label="Enviar formulário">Submit</button>
    </form>

    <div class="success-message" v-if="successMessage" aria-live="polite">
      {{ successMessage }}
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const firstName = ref("");
const lastName = ref("");
const email = ref("");
const queryType = ref("generalEnquiry");
const message = ref("");
const consent = ref(false);
const firstNameErrors = ref("");
const lastNameErrors = ref("");
const emailErrors = ref("");
const messageErrors = ref("");
const successMessage = ref("");

const handleSubmit = async () => {
  firstNameErrors.value = "";
  lastNameErrors.value = "";
  emailErrors.value = "";
  messageErrors.value = "";

  if (!firstName.value) {
    firstNameErrors.value = "Por favor, preencha o primeiro nome.";
  }
  if (!lastName.value) {
    lastNameErrors.value = "Por favor, preencha o sobrenome.";
  }
  if (!email.value || !validateEmail(email.value)) {
    emailErrors.value = "Por favor, digite um e-mail válido.";
  }
  if (!message.value) {
    messageErrors.value = "Por favor, escreva sua mensagem.";
  }
  if (!consent.value) {
    console.warn("Usuário não consentiu com o contato.");
  }

  if (
    firstNameErrors.value ||
    lastNameErrors.value ||
    emailErrors.value ||
    messageErrors.value
  ) {
    return;
  }

  successMessage.value = "Formulário enviado com sucesso!";
  firstName.value = "";
  lastName.value = "";
  email.value = "";
  queryType.value = "generalEnquiry";
  message.value = "";
  consent.value = false;

  console.log("Formulário enviado com sucesso!");
};

const validateEmail = (email) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
};
</script>

<style scoped>
.container {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  background-color: #f0f8f7;
  padding: 40px;
}

.title {
  margin-bottom: 20px;
  text-align: center; /* Centraliza o título */
  font-size: 24px;
  font-weight: bold;
  color: #333;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.form-row {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.form-group {
  margin-bottom: 20px;
  flex: 1;
}

label {
  display: block;
  margin-bottom: 10px; /* Aumenta o espaço entre o label e o input */
  font-weight: bold;
  color: #555;
  text-align: left; /* Alinha os labels à esquerda */
}

input[type="text"],
input[type="email"],
select,
textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  background-color: #f8f8f8;
  color: #555;
  transition: border-color 0.3s ease;
}

textarea {
  height: 100px;
  resize: vertical;
}

input[type="checkbox"] {
  margin-right: 10px;
}

button[type="submit"] {
  background-color: #008060;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  width: 100%;
}

button[type="submit"]:hover {
  background-color: #006b4f;
}

.error {
  color: red;
  font-size: 14px;
  margin-top: 5px;
}

.success-message {
  margin-top: 20px;
  color: green;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
}

.radio-group {
  display: flex;
  gap: 20px;
}

.radio-group label {
  display: flex;
  align-items: center;
  gap: 5px;
  text-align: left;
}

.checkbox-group {
  display: flex;
  align-items: center;
  gap: 10px;
}

/* Responsivo */
@media (max-width: 600px) {
  .form-row {
    flex-direction: column;
  }

  .form-group {
    width: 100%;
  }

  .radio-group {
    flex-direction: column;
  }
}
</style>
