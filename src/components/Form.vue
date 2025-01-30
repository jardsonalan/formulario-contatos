<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import { ref } from 'vue';

const pararEnvio = (evt:Event) => {
  evt.preventDefault()
}

const nome = ref('')
const email = ref('')

console.log(nome, email)
</script>

<template>
  <form class="form-cadastro" @submit="pararEnvio">
    <div class="nome-input">
      <label for="nome">Nome</label>
      <input type="text" id="nome" v-model="nome">
    </div>
    <div class="email-input">
      <label for="email" id="email">E-mail</label>
      <input type="text" id="email" v-model="email">
    </div>
    <button @click="$emit('cadastrar', nome, email)">Cadastrar</button>
  </form>
</template>

<style scoped>
  .form-cadastro {
    background-color: rgb(132, 181, 255);
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .form-cadastro > .nome-input, .form-cadastro > .email-input {
    display: flex;
    flex-direction: column;
    width: 80%;
    margin: 0 auto;
  }

  .form-cadastro > .nome-input > input, .form-cadastro > .email-input > input {
    padding: 4px;
  }

  .form-cadastro > button {
    margin: 10px 0 0 0;
    padding: 6px;
    width: 80%;
    cursor: pointer;
  }
</style>
