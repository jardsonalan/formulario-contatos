<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import { ref } from 'vue';
import { VTextField } from 'vuetify/components';

const nome = ref('')
const email = ref('')

const pararEnvio = (evt:Event) => {
  evt.preventDefault()
  nome.value = ''
  email.value = ''
}

</script>

<template>
    <VForm class="mt-8" @submit="pararEnvio">
      <VTextField type="text" id="nome" v-model="nome" label="Nome"/>

      <VTextField type="text" id="email" v-model="email" label="E-mail"/>

      <VBtn class="w-100" prepend-icon="mdi-plus-circle-outline" @click="$emit('cadastrar', nome, email)">Cadastrar</VBtn>
    </VForm>
</template>

<style scoped>
  /* .form-cadastro {
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .form-cadastro > .nome-input, .form-cadastro > .email-input {
    display: flex;
    flex-direction: column;
    width: 80%;
    margin: 5px 0;
  }

  .form-cadastro > .nome-input > label, .form-cadastro > .email-input > label {
    color: white;
    margin: 0 0 8px 0;
    font-weight: bold;
  }

  .form-cadastro > .nome-input > input, .form-cadastro > .email-input > input {
    padding: 5px;
    font-size: 16px;
    border: none;
  }

  .form-cadastro > button {
    margin: 10px 0 0 0;
    padding: 8px;
    width: 80%;
    cursor: pointer;
    border: none;
    background-color: #2c7553;
    color: white;
    font-weight: bold;
    font-size: 17px;
  } */
</style>
