<template>
  <div class="filme-container">
    <h2>Cadastro de Filmes</h2>

    <!-- Mensagem caso a lista esteja vazia -->
    <p v-if="filmes.length === 0">Nenhum filme cadastrado ainda.</p>

    <!-- Formulário de Cadastro -->
    <div class="input-group">
      <input v-model="novoFilme.titulo" placeholder="Título do Filme" />
      <input v-model="novoFilme.genero" placeholder="Gênero" />
      <input v-model="novoFilme.ano" placeholder="Ano de Lançamento" type="number" />
      <button @click="adicionarFilme">Adicionar Filme</button>
    </div>

    <!-- Lista de Filmes -->
    <ul>
      <li v-for="(filme, index) in filmes" :key="index">
        <span>{{ filme.titulo }} - {{ filme.genero }} - {{ filme.ano }}</span>
        <button @click="deletarFilme(index)">Deletar</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const novoFilme = ref({ titulo: '', genero: '', ano: '' })
const filmes = ref([])

const adicionarFilme = () => {
  if (novoFilme.value.titulo && novoFilme.value.genero && novoFilme.value.ano) {
    filmes.value.push({ ...novoFilme.value })
    limparCampos()
  } else {
    alert('Por favor, preencha todos os campos.')
  }
}

const deletarFilme = (index) => {
  filmes.value.splice(index, 1)
}

const limparCampos = () => {
  novoFilme.value = { titulo: '', genero: '', ano: '' }
}
</script>

<style scoped>
.filme-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f9;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
h2 {
  text-align: center;
  color: #333;
}
.input-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}
.input-group input {
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}
.input-group button {
  padding: 10px;
  font-size: 1rem;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.input-group button:hover {
  background-color: #0056b3;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-bottom: 10px;
}
li span {
  font-size: 1rem;
}
li button {
  padding: 5px 10px;
  background-color: #dc3545;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
li button:hover {
  background-color: #c82333;
}
</style>
