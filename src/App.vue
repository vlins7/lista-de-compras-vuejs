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

</style>
