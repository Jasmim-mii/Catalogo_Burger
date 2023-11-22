<template>
    <MessageForm :msg="msg" v-show="msg" />

    <div class="main-container">
        <div class="forms">
            <form id="burger-form" @submit="createdBurger">
                <div class="input-container">
                    <label for="name">Nome do cliente:</label>
                    <input type="text" name="name" id="name" v-model="name" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="bun">Escolha o pão:</label>
                    <select name="bun" id="bun" v-model="bun" value="">
                        <option value="">Selecione seu pão</option>
                        <option v-for="bun in buns" :key="bun.id" :value="bun.type"> {{ bun.type }}
                        </option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="burger">Escolha a carne do seu Burger:</label>
                    <select name="burger" id="burger" v-model="burger" >
                        <option value="">Selecione sua carne</option>
                        <option v-for="burge in productBurger" :key="burge.id" :value="burge.type" >{{ burge.type }}</option>
                    </select>
                </div>
                <div id="ingrents-container" class="input-container">
                    <label id="title" for="ingredients">Mais ingredientes:</label>
                    <div class="checkbox-container" v-for="ingredient in ingredientsData" :key="ingredient.id" :value="ingredient.type" >
                        <input type="checkbox" name="ingredients"  v-model="ingredients" :value="ingredient.type">
                        <span>{{ ingredient.type }}</span>
                    </div>
                </div>
                <div class="input-container">
                  <input type="submit" class="submit-btn" value="Finalizar Burger">
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import MessageForm from './MessageForm.vue'

export default {
    name: 'BurgerForm',
    components: { 
        MessageForm, 
    },
    data(){
        return{
            buns: null,
            productBurger: null,
            ingredientsData: null,
            name: null,
            bun: null,
            burger: null,
            ingredients: [],
            msg: null,
        }  
    },
    methods: {
        // pegar ingredientes
        async getIngrents() {
            const req = await fetch('https://api-brugers.vercel.app/ingredientes');
            const data = await req.json();

            this.buns = data.buns;
            this.productBurger = data.productBurger;
            this.ingredientsData = data.ingredients;

        },

        async createdBurger(e){
            e.preventDefault();
            const data = {
                name: this.name,
                burger: this.burger,
                bun: this.bun,
                ingredients: Array.from(this.ingredients),
                status: 'Solicitado'
            }

            // transformando json em string e adicionar em burgers no db.json
            const dataJson = JSON.stringify(data)

            const req =await fetch('https://api-brugers.vercel.app/burgers', {
                method: 'POST',
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });
            const response = await req.json()

            //colocar msg
            this.msg = `Pedido Nº ${response.id} realizado com sucesso`

            //limpar msg
            setTimeout(() => this.msg = "", 3000);

            //limpar dados]
            this.name = "";
            this.bun = "";
            this.burger = "";
            this.ingredients = "";

            console.log(response);

        }
       
    },
    mounted() {
        this.getIngrents()
    }
}
</script>

<style scoped>
#burger-form{
    max-width: 25rem;
    margin: 0 auto;
}
.input-container{
    display: flex;
    flex-direction: column;
    padding-bottom: 1.5rem;
}
label{
    font-weight: bold;
    margin-bottom: .7rem;
    color: #222;
    padding: .2rem .7rem;
    border-left: .2rem solid #fcba03
}
input, select{
    padding: .5rem .7rem;
}
#ingrents-container{
    flex-direction: row;
    flex-wrap: wrap;
}
.checkbox-container{
    display: flex;
    align-items: flex-start;
    width: 30%;
    margin-bottom: 1rem;
}
.checkbox-container span,
.checkbox-container input{
    padding: 0 .3rem 0 .4rem;
    font-weight: 700;
    color: #2e2e2e
}
#title{
    width: 100%;
}
.submit-btn{
    background: #222;
    color: #fcba03;
    font-weight: 700;
    border: .1rem solid #222;
    padding: 1rem 3rem;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s
}
.submit-btn:hover{
    color: #fcba03;
    transform: scalex(1.1)
}

</style>