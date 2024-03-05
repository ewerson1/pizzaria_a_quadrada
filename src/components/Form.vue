<template>
  <p>Mensagem</p>
  <div>
    <form id="pizza-form">
      <div class="input-container">
        <label for="nome">Nome do cliente:</label>
        <input type="text" id="nome" name="nome" v-model="nome" />
      </div>

      <div class="input-container">
        <label for="massa">Escolha a massa:</label>
        <select name="massa" id="massa" v-model="massa">
          <option value="">normal</option>
          <option value="intaliana">intaliana</option>
        </select>
      </div>

      <div class="input-container">
        <label for="sabores">escolha até 2 sabores:</label>
        <select name="sabores" id="sabores" v-model="sabores">
          <option value="">sabores</option>
          <option value="baiana">Baiana</option>
        </select>
      </div>

      <div class="input-container">
        <label for="opcionais">selecione os opcionais: </label>
       <div class="checkbox-container">
        <input type="checkbox" name="opcionais"
        v-model="opcionais" value="cheddar">
        <span> cheddar</span>
       </div>
      </div>

      <div class="input-container">
        <input type="submit" class="submit-btn" value="montar minha pizza!">
        
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Form",
};
</script>

<style scoped>
  #pizza-form {
    max-width: 400px;
    margin: 0 auto;
  }
  
  .input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }


</style>
