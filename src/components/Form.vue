<template>
 
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

      <div class="input-container" id="opicionais-container">
        <label id="opcionais-title" for="opcionais">selecione os opcionais: </label>

       <div class="checkbox-container">
        <input type="checkbox" name="opcionais"
        v-model="opcionais" value="cheddar">
        <span> cheddar</span>
       </div>

       <div class="checkbox-container">
        <input type="checkbox" name="opcionais"
        v-model="opcionais" value="Catupiry">
        <span> Catupiry</span>
       </div>

       <div class="checkbox-container">
        <input type="checkbox" name="opcionais"
        v-model="opcionais" value="salsicha">
        <span> salsicha</span>
       </div>
       <div class="checkbox-container">
        <input type="checkbox" name="opcionais"
        v-model="opcionais" value="Ovos">
        <span> Ovos</span>
       </div>
      </div>

      <div class="input-container">
        <input type="submit" class="submit-btn" value="Montar minha pizza!">
        
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

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px ;
    border-left: 4px solid #fcba03;
  }

  input, select{
    padding: 5px 10px;
    width: 300px;
  }

  #opicionais-container{
    flex-direction: row;
    flex-wrap: wrap;

  }

  #opicionais-title{
    width: 100%;
  }

  .checkbox-container{
    display: flex;
    align-items: center;
    width: 50%;
    margin-bottom: 20px;

  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn{
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover{
    background-color: #fcba03 ;
    color: #222;
  }


</style>
