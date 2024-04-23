<script setup>
  import {ref} from "vue";

  const inputValue = ref('');
  const number = ref([]);
  const ErrorMessage = ref("")

  const format = (cpf) => {
    return cpf.replace(/\D/g, '');
  };

  const validateInput = () => {
    const validCPF = format(inputValue.value);

    if (validCPF.length === 11) {
    const formatCPF = validCPF.replace(/(\d{3})(\d{3})(\d{3})(\d{2})/, '$1.$2.$3-$4');
      number.value.push({
      text: formatCPF });
      ErrorMessage.value = "";

    } else { 
      ErrorMessage.value = "CPF NEEDS 11 CHARACTERS"
    }
    
  };

  const applyMask = () => {
    inputValue.value = inputValue.value
    .replace(/\D/g, '')
    .replace(/(\d{3})(\d{3})(\d{3})(\d{2})/, '$1.$2.$3-$4');

    inputValue.value = inputValue.value.slice(0, 14)
  
  };
</script>

<template>
<main>
  <header class="title">
    <h1>Autenticador de CPF</h1>
  </header>
  <div class="header">
    Digite seu CPF: <input type="text" class="boxtext" v-model="inputValue" @input="applyMask">
    <button class="validator" @click="validateInput">Validar</button>
  </div>
  <div class="list">
    <ul>
      <p class="error" v-if="ErrorMessage">{{ ErrorMessage }}</p>
      <li v-for="item in number" :key="item.text">
        {{ item.text }}
      </li>
    </ul>
  </div>
</main>
</template>

<style scoped>
  main {
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  h1 {
    display: flex;
    align-items: center;
    font-weight: bold;
    margin: 55px 0px 35px 0px;
    font-size: 45px;
    color: rgba(137, 43, 226, 0.556);
  }

  header {
    align-items: center;
    display: flex;
  }
  .boxtext {
  box-shadow: 1px 1px 1px 1px rgba(224, 8, 224, 0.633);
  }
  .validator {
    background-color: rgb(137, 43, 226);
    margin: 0px 8px;
    font-size: 16px;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  }

  li {
    color: blueviolet;
    font-size: 25px;
  }
  .error {
    color: red;
    padding: 0px 0px 12px 0px;
  }
</style>


