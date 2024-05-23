<template>
  <div class="container">
    <FormTitle />

    <form @submit.prevent="handleSubmit">
      <FormRow>
        <FormGroup
          for="firstName"
          label="First Name *"
          :errors="firstNameErrors"
        >
          <input
            type="text"
            id="firstName"
            name="firstName"
            v-model="firstName"
            required
            aria-label="Primeiro nome"
          />
        </FormGroup>
        <FormGroup for="lastName" label="Last Name *" :errors="lastNameErrors">
          <input
            type="text"
            id="lastName"
            name="lastName"
            v-model="lastName"
            required
            aria-label="Sobrenome"
          />
        </FormGroup>
      </FormRow>

      <FormGroup for="email" label="Email Address *" :errors="emailErrors">
        <input
          type="email"
          id="email"
          name="email"
          v-model="email"
          required
          aria-label="E-mail"
        />
      </FormGroup>

      <FormGroup label="Query Type *">
        <RadioGroup
          :options="queryOptions"
          name="queryType"
          v-model="queryType"
          required
        />
      </FormGroup>

      <FormGroup for="message" label="Message *" :errors="messageErrors">
        <textarea
          id="message"
          name="message"
          v-model="message"
          required
          aria-label="Mensagem"
        ></textarea>
      </FormGroup>

      <CheckboxGroup
        id="consent"
        name="consent"
        label="I consent to being contacted by the team *"
        v-model="consent"
        required
      />

      <button type="submit" aria-label="Enviar formulário">Submit</button>
    </form>

    <SuccessMessage v-if="successMessage" :message="successMessage" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import FormTitle from "./components/FormTitle.vue";
import FormGroup from "./components/FormGroup.vue";
import FormRow from "./components/FormRow.vue";
import RadioGroup from "./components/RadioGroup.vue";
import CheckboxGroup from "./components/CheckboxGroup.vue";
import SuccessMessage from "./components/SuccessMessage.vue";

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

const queryOptions = [
  { value: "generalEnquiry", label: "General Enquiry" },
  { value: "supportRequest", label: "Support Request" },
];

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

/* Responsivo */

@media (max-width: 600px) {
  .container {
    padding: 10px;
  }

  button[type="submit"] {
    font-size: 14px;
  }

  .title {
    font-size: 20px;
  }

  .form-group {
    gap: 10px;
  }

  .form-group label {
    font-size: 16px;
  }

  .form-row {
    gap: 10px;
  }

  .error {
    font-size: 12px;
  }

  .success-message {
    font-size: 14px;
  }

  .checkbox-group {
    gap: 10px;
  }

  .checkbox-group label {
    font-size: 16px;
  }

  .radio-group {
    gap: 10px;
  }

  .radio-group label {
    font-size: 16px;
  }

  .radio-group input[type="radio"] {
    width: 20px;
    height: 20px;
  }

  .radio-group input[type="radio"] + label {
    font-size: 16px;
  }

  .form-group input[type="text"],
  .form-group input[type="email"],
  .form-group textarea {
    font-size: 16px;
  }
}
</style>
