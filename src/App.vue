<script setup>
  import { ref } from 'vue';

  const itensLista = ref([]);
  const novoItemInput = ref('');

  function adicionarNovoItem() {    
    if(novoItemInput.value.trim() !== '') {
      let newId = 1;

      if (itensLista.value.length > 0) {
        const maxId = itensLista.value.reduce((max, item) => {
          return item.id > max ? item.id : max
        }, -Infinity)
        
        newId = maxId + 1;
      } 
      
      const newItemToAdd = {
        id: newId,
        value: novoItemInput.value
      }

      itensLista.value.push(newItemToAdd);
      novoItemInput.value = '';
    }
  }

  function removerItem(id) {
    itensLista.value = itensLista.value.filter(item => item.id !== id);
  }
</script>

<template>
  <div class="container">
    <h1>Lista de compras</h1>

    <p>Adicione seus produtos à lista</p>

    <span>Total de itens: {{ itensLista.length   }}</span>

    <div class="user-interaction">
      <input type="text" placeholder="Digite o nome do produto" v-model="novoItemInput" @keyup.enter="adicionarNovoItem">

      <button @click="adicionarNovoItem">Adicionar</button>
    </div>


    <div class="cesta-de-compras">
      <p v-if="itensLista.length > 0">Minha Cesta de Compras</p>
      <p v-else>Sua cesta está vazia! Adicione produtos para começar.</p>

      <ul>
        <li v-for="item in itensLista" :key="item.id">
          {{ item.value }}

          <button @click="removerItem(item.id)">🗑️</button>
        </li>
      </ul>
    </div>    
  </div>
</template>

<style scoped>
.container {
    max-width: 480px;
    margin: 40px auto;
    padding: 24px;
    font-family: 'Segoe UI', Arial, sans-serif;
    background: #fffef8;
    border: 1px solid #eee;
    border-radius: 8px;
  }

  h1 {
    margin-bottom: 4px;
  }

  p {
    color: #777;
    margin-bottom: 12px;
  }

  span {
    font-size: 13px;
    color: #aaa;
  }

  .user-interaction {
    display: flex;
    gap: 8px;
    margin: 16px 0 20px;
  }

  input {
    flex: 1;
    padding: 10px;
    border: none;
    border-bottom: 2px solid #ddd;
    background: transparent;
    outline: none;
  }

  input:focus {
    border-color: #333;
  }

  button {
    padding: 8px 12px;
    border: none;
    background: #333;
    color: white;
    border-radius: 6px;
    cursor: pointer;
  }

  ul {
    list-style: none;
    padding: 0;
    margin-top: 10px;
  }

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 4px;
    border-bottom: 1px dashed #ddd;
    font-size: 15px;
    list-style: none;
  }

  li button {
    background: transparent;
    color: #bbb;
    font-size: 16px;
    padding: 4px;
  }

  li button:hover {
    color: #e74c3c;
  }
</style>
