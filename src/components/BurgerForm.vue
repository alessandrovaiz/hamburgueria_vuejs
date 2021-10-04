<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form  id="burger-form" @submit="createOrder">
                <div class="input-container">
                    <label for="name">
                        Nome do cliente : 
                    </label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Nome do cliente">
                </div>

                 <div class="input-container">
                    <label for="bread">
                        Escolha o pão : 
                    </label>
                    <select name="bread" id="bread" v-model="bread">
                        <option value="" selected>Selecione o pão</option>
                        <option v-for="bread in breads" :value="bread.type" :key="bread.id">
                            {{ bread.type }}                            
                        </option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="meat">
                        Escolha a carne : 
                    </label>
                    <select name="meat" id="meat" v-model="meat">
                        <option value="" selected>Selecione a carne</option>
                        <option v-for="meat in meats" :value="meat.type" :key="meat.id">{{ meat.type }}</option>
                    </select>
                </div>

                 <div class="optionals-container input-container">
                    <label for="optionals" id="optionals-title">
                        Selecione os ingredientes optionals : 
                    </label>
                    <div class="checkbox-container" v-for="optional in dataOptionals" :key="optional.id">
                        <input type="checkbox" name="optionals" v-model="optionals" :value="optional.type">
                        <span>{{ optional.type }}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu hamburguer">
                </div>


            </form>
        </div>
    </div>
</template>

<script>
import Message from '../components/Message.vue'
export default {
    name:'BurgerForm',
    components: {
        Message
    },
    data() {
        return {
            breads: null,
            meats: null,
            dataOptionals: null,

            name: null,
            bread: null,
            meat:null,
            optionals:[],
            msg: null

        }
    },
    methods: {
        async fetchIngredients() {

            const req = await fetch('http://localhost:3000/ingredientes')
            const data = await req.json();

            this.breads = data.breads
            this.meats = data.meats
            this.dataOptionals = data.optionals
            
        },

        async createOrder(event) {
            event.preventDefault()

            const data = {
                name: this.name,
                meat : this.meat,
                bread : this.bread,
                optionals: Array.from(this.optionals),
                status : 'Solicitado'
            }

            const dataJson = JSON.stringify(data)

            const req = await fetch('http://localhost:3000/orders', {
                method:"POST",
                headers: {
                    "Content-type": "application/json"
                },
                body: dataJson
            })

            const res = await req.json()

            this.msg = `Pedido nº ${res.id} realizado com sucesso`

            setTimeout(() => this.msg = '', 3500)

            this.name = ''
            this.bread = ''
            this.meat = ''
            this.optionals = ''

        }
    },
    mounted() {
        this.fetchIngredients()
    }
}
</script>

<style scoped>
    #burger-form {
        max-width:400px;
        margin: 0 auto;
    }

    .input-container {
        display:flex;
        flex-direction:column;
        margin-bottom:20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select {
        padding: 5px 10px;
        width: 400px;
    }

    .optionals-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #optionals-title {
        width: 100%;
    }

    .checkbox-container {
        display:flex;
        align-items: flex-start;
        width:50%;
        margin-bottom:20px;
    }

    .checkbox-container span, .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight:bold;
        border: 2px solid #222;
        padding:10px;
        font-size:16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s;
    }

    .submit-btn:hover {
        background-color : transparent;
        color: #222;
    }



</style>