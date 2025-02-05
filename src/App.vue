<script setup lang="ts">
import Form from './components/Form.vue';
import { ref, onMounted } from 'vue';
import axios from 'axios';

type Dados = {
  id: number,
  nome: string,
  email: string
}

const listaDados = ref<Dados[]>([])

async function adicionarPessoas (nome: string, email: string) {
  if (nome !== '' && email !== '') {
    // listaDados.value.push({
    //   nome: nome,
    //   email: email
    // })

    await axios.post('http://localhost:3000/contatos', {
      nome,
      email,
    })

    await listarContatos()
  }
}

async function listarContatos() {
  const resultado = await axios.get('http://localhost:3000/contatos')

  if (resultado.status === 200) {
    listaDados.value = resultado.data
  }
  // console.log(resultado)
}

async function deletarContatos(id: number) {
  await axios.delete(`http://localhost:3000/contatos/${id}`)

  await listarContatos()
}

onMounted(listarContatos)
</script>

<template>
  <Form
    @cadastrar="adicionarPessoas"
  />
  <div class="container-tabela">
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
          <button @click="deletarContatos(item.id)">Deletar</button>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.container-tabela {
  height: 300px;
  overflow-y: auto;
  margin: 10px 0 0 0;
}

table {
  width: 80%;
  color: #ffffff;
  text-align: center;
  border-collapse: collapse;
  margin: 0px auto;
  background-color: #4b9673;
}

table th {
  position: sticky;
  top: 0;
  background-color: #327a58;
  color: #8becbf;
}

table td, table th {
  border: 1px solid #a1ecc9;
  padding: 8px;
  font-size: 16px;
}
</style>
