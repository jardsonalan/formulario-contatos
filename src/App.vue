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
  <VContainer>
    <VRow justify="center">
      <VCol cols="6">
        <Form
          @cadastrar="adicionarPessoas"
        />
      </VCol>
    </VRow>
    <VRow>
      <VCol>
        <h2 class="text-center mt-5">Lista de Contatos</h2>
        <div class="container-tabela mt-3">
          <VTable>
            <thead>
              <tr>
                <th class="text-center border">Nome</th>
                <th class="text-center border">E-mail</th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(item, index) in listaDados"
                :key="index"
              >
                <td class="text-center border">
                  {{ item.nome }}
                </td>
                <td class="text-center border">
                  {{ item.email }}
                </td>
                <td><VBtn icon="mdi-delete" density="compact" color="error" variant="text" @click="deletarContatos(item.id)"/></td>
              </tr>
            </tbody>
          </VTable>
        </div>
      </VCol>
    </VRow>
  </VContainer>
</template>

<style scoped>
.container-tabela {
  height: 300px;
  overflow-y: auto;
}

/* .container-tabela {
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


table td, table th {
  border: 1px solid #a1ecc9;
  padding: 8px;
  font-size: 16px;
  } */

  table th {
    background-color: #327a58;
    color: #8becbf;
  }
</style>
