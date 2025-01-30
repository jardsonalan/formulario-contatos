<script setup lang="ts">
import Form from './components/Form.vue';
import { ref } from 'vue';

type Dados = {
  nome: string,
  email: string
}

const listaDados = ref<Dados[]>([])

const adicionarPessoas = (nome: string, email: string) => {
  listaDados.value.push({
    nome: nome,
    email: email
  })
}
</script>

<template>
  <Form
    @cadastrar="adicionarPessoas"
  />
  <table>
    <thead>
      <tr>
        <th>Nome</th>
        <th>E-mail</th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="(item, index) in listaDados"
        :key="index"
      >
        <td>
          {{ item.nome }}
        </td>
        <td>
          {{ item.email }}
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>

</style>
