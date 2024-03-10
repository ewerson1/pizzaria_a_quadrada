<template>
  <div>
    <Message :msg="msg" v-show="msg"/>
    <form id="pizza-form" @submit="createPizza">
      <div class="input-container">
        <label for="nome">Nome do cliente:</label>
        <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome"/>
      </div>

      <div class="input-container">
        <label for="massa">Escolha a massa:</label>
        <select name="massa" id="massa" v-model="massa">
          <option v-for="massa in massas" :key="massa.id" :value="massa.tipo">
            {{ massa.tipo }}
          </option>
        </select>
      </div>

      <div class="input-container">
        <label for="sabor">Escolha o sabor: </label>
        <select name="sabor" id="sabor" v-model="sabor">
          <option v-for="sabor in sabores" :key="sabor.id" :value="sabor.tipo">
            {{ sabor.tipo }}
          </option>
        </select>
      </div>

      <div class="input-container" id="opcionais-container">
        <label id="opcionais-title" for="opcionais"
          >selecione os opcionais:
        </label>
        <div
          class="checkbox-container"
          v-for="opcional in opcionaisdata"
          :key="opcional.id"
          :value="opcional.tipo"
        >
          <input
            type="checkbox"
            name="opcionais"
            v-model="opcionais"
            :value="opcional.tipo"
          />
          <span> {{ opcional.tipo }}</span>
        </div>
      </div>

      <div class="input-container">
        <input type="submit" class="submit-btn" value="Montar minha pizza!" />
      </div>
    </form>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
  name: "Form",
  components:{
    Message
  },
  data() {
    return {
      massas: null,
      sabores: null,
      opcionaisdata: null,
      nome: null,
      
      massa: null,
      sabor: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
       // buscando dados no servidor e usando (await) para esperar os dados chegar
      const req = await fetch("http://localhost:3000/ingredientes ");

       // transformando o req em json e usando (await) para esperar transformar
      const data = await req.json();

       // transformando os dados da "req" nos dados criandos no DATA 
      this.massas = data.massas;
      this.sabores = data.sabores;
      this.opcionaisdata = data.opcionais;
    },

    async createPizza(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        sabores: this.sabor,
        massas: this.massa,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };

      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/pizzas", {
        method: "POST",
        Headers: {"content-type": "application/json"},
        body: dataJson
      });

      const res = await req.json();

      // pedido realizado
      this.msg = `Pedido Nº ${res.id} realizado com sucesso ✅`;
      // limpar msg
      setTimeout(() => this.msg = "", 3000);

      // limpar campos
      this.nome = "";
      this.massa = "";
      this.sabor = "";
      this.opcionais = "";


    },
  },
  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>
#pizza-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#opcionais-title {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: center;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}

.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}

.submit-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.submit-btn:hover {
  background-color: #fcba03;
  color: #222;
}
</style>
