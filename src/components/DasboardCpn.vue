<template>
    <MessageForm :msg="msg" v-show="msg" />

    <div id="burger-table">
        <h1>Dasboard</h1>
        <div>
            <div id="burger-table-heading">
                <div class="order-id">
                    <div>id</div>
                    <div>Cliente:</div>
                    <div>Pão:</div>
                    <div>Carne:</div>
                    <div>Ingredientes:</div>
                    <div>Ações:</div>
                </div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div class="burger-table-row" v-for="burger in burgers" :key="burger.id" >
                <div class="order-number">
                    <div id="id">{{burger.id}}</div>
                    <div>{{burger.name}}</div>
                    <div>{{burger.bun}}</div>
                    <div>{{burger.burger}}</div>
                    <div>
                        <span v-for="(opcional, index) in burger.ingredients" :key="index">
                            <li>{{ opcional }}</li>
                        </span>
                        
                    </div>           
                    <div>
                        <select  name="status" class="status btn" @change="updateBurger($event, burger.id)">
                            <option>Selecione</option>
                            <option v-for="i in status" :key="i.id" :value="i.type" :selected="burger.status == i.type">{{ i.type }}</option>
                        </select>
                        <button class="delete-btn btn" @click="deleteBurger(burger.id)">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import MessageForm from './MessageForm.vue'

export default {
    name: 'DasboardCpn',
    components: {
        MessageForm, 
    },
    data(){
        return{
            burgers: null,
            burger_id: null,
            status: [],
            msg: null,
        }
    },
    methods: {

        // buscando os burges em pedidos
        async getList(){
            const req = await fetch("https://api-brugers.vercel.app/burgers");
            const data = await req.json()

            this.burgers = data;

            //resgantando status
            this.getStatus();

        },

        //buscando status pedido
        async getStatus(){
            const req = await fetch("https://api-brugers.vercel.app/status");
            // transformando em data
            const data = await req.json();

            this.status = data;
        },

        //deletar
        async deleteBurger(id){
            const req = await fetch(`https://api-brugers.vercel.app/burgers/${id}`, {
                method: "DELETE",
            
            });
            const res = await req.json();

            //colocar msg
            this.msg = ` Pedido removido com sucesso`

            //limpar msg
            setTimeout(() => this.msg = "", 3000);

            this.getList();

            console.log(res)
        },

        async updateBurger(event, id){
            const option = event.target.value;
            const dataJson = JSON.stringify( {status: option})
            const req = await fetch(`https://api-brugers.vercel.app/burgers/${id}`,{
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const response = await req.json();
             //colocar msg
             this.msg = ` Pedido  Nº ${response.id} Atualizado para ${response.status}`

            //limpar msg
            setTimeout(() => this.msg = "", 3000);

            console.log(response)

        }
    },
   
    //chamando os bugers
    mounted(){
        this.getList();
    }
}
</script>

<style scoped>
#burger-table{
    max-width: 100%;
    margin: 0 ;
}
.order-number,
.order-id {
    display: grid;
    grid-template-columns: max-content 1fr 1fr 1fr 3.5fr 3fr ;
    font-size: .9rem;
    font-weight: 600;
}
.order-number span li{
    font-size: .8rem;
    font-weight: 550;
    display: inline-block;
    border: .1rem solid #ccc;
    padding: .5rem .8rem;
    margin: .1rem;
    transition: .3s;
}
.order-number span li:hover{
    background: #ccc;
    color: #000
}
#burger-table-heading{
    font-weight: bold;
    padding: 1rem;
    border-bottom: .3rem solid #333;
}
#burger-table-heading div,
.burger-table-row div {
    column-gap: 3rem;
}
.burger-table-row{
    width: 100%;
    padding: 1rem;
    border-bottom: .1rem solid #ccc
}
.btn{
    padding: .6rem .8rem;
    margin-right:.8rem ;
    font-weight: 550;
    font-size: .8rem;
    text-align: center;
    border: none;
    cursor: pointer;
    width: 110px 
}
.delete-btn{
    background: #000;
    color: #fcba03;
    border-radius: .2rem;
    transition: .3s;
    margin: 0 auto
}
.delete-btn:hover{
    background: #3f0303;
    color: #ececec
}
.status{
    background: #d4d4d4;
    border-radius: .2rem;
}

</style>