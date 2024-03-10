<template>
  <div id="pizza-table">
    <Message :msg="msg" v-show="msg"/>
        <div>
            <div id="pizza-table-heading">
                <div id="order-id">#:</div>
                <div>Cliente:</div>
                <div>Massa:</div>
                <div>Sabor:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
        </div>
        <div id="pizza-table-rows">
            <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id">
                <div class="order-number">{{ pizza.id }}</div>
                <div>{{ pizza.nome }}</div>
                <div>{{ pizza.massas }}</div>
                <div>{{ pizza.sabores }}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in pizza.opcionais" :key="index"> {{ opcional }}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updatePizza ($event,pizza.id)" >
                    <option  v-for="s in status" :key="s.id" :value="s.tipo" :selected="pizza.status == s.tipo" >{{ s.tipo }} </option>
                   
                    </select>
                   
                    <button class="delete-btn" @click="deletePizza(pizza.id)">Cancelar</button>
                </div>
            </div>
        </div>

  </div>
</template>

<script>
import Message from "./Message.vue"
export default {
  name: "Dashboard",
  data(){
    return{
        pizzas: null,
        pizzas_id: null,
        status: [],
        msg: null
    }
   },
   components:{
    Message
   },

   methods: {
    async getPedidos (){
        // buscando dados no servidor e usando (await) para esperar os dados chegar
        const req = await fetch("http://localhost:3000/pizzas");

        // transformando o req em json e usando (await) para esperar transformar
        const data = await req.json();

        // transformando os dados da "req" em "pizzas" criado no data
        this.pizzas = data;

        // resgatar status
        this.getStatus();
    },
    async getStatus(){
        // buscando dados no servidor e usando (await) para esperar os dados chegar
        const req = await fetch("http://localhost:3000/status");

        // transformando o req em json e usando (await) para esperar transformar  
        const data = await req.json();

        // transformando os dados da "req" em "pizzas" criado no data
        this.status = data;
   },

   async deletePizza(id){
        const req = await fetch(`http://localhost:3000/pizzas/${id}`,{
            method: "DELETE"
        });

        const res = await req.json();


        // msg ao cancelar pedido
        this.msg = `Pedido Nº ${res.id} removido com sucesso ✅`;
        // limpar msg
        setTimeout(() => this.msg = "", 3000);
        
        this.getPedidos();
   },

   async updatePizza(event, id){
        const option = event.target.value;


        const dataJson= JSON.stringify({status: option});

        const req = await fetch (`http://localhost:3000/pizzas/${id}`, {
            method: "PATCH",
            headers: {"Content-Type": "application/json" },
            body: dataJson
        });

        const res = await req.json();

         // msg ao cancelar pedido
         this.msg = `Pedido Nº ${res.id} atualizado para ${res.status} `;
        // limpar msg
        setTimeout(() => this.msg = "", 3000);
        
        this.getPedidos();

        console.log(res)


   }

},
//    quando o componente for montado
   mounted(){
    this.getPedidos();
   },
  
};

</script>



<style scoped>
#pizza-table {
  max-width: 1280px;
  margin: 0 auto;
}
#pizza-table-heading,
#pizza-table-rows,
.pizza-table-row{
    display: flex;
    flex-wrap: wrap;
}

#pizza-table-heading{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid;
}
#pizza-table-heading div,
.pizza-table-row div{
    width: 19%;
}

.pizza-table-row{
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
}

#pizza-table-heading #order-id,
.pizza-table-row .order-number{
    width: 5%;
}

select{
    padding: 12px 6px;
    margin-right: 12px;
    border-radius: 0;
}

.delete-btn{
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.delete-btn:hover{
    background-color: #fcba03;
    color: #222;
}

</style>
