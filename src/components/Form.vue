<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import { ref } from 'vue';

const nome = ref('')
const email = ref('')

const pararEnvio = (evt:Event) => {
  evt.preventDefault()
  nome.value = ''
  email.value = ''
}

</script>

<template>
  <form class="form-cadastro" @submit="pararEnvio">
    <div class="nome-input">
      <label for="nome">Nome</label>
      <input type="text" id="nome" v-model="nome" placeholder="Informe seu nome">
    </div>
    <div class="email-input">
      <label for="email" id="email">E-mail</label>
      <input type="text" id="email" v-model="email" placeholder="Informe seu e-mail">
    </div>
    <button @click="$emit('cadastrar', nome, email)">Cadastrar</button>
  </form>
</template>

<style scoped>
  .form-cadastro {
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
  }
</style>
