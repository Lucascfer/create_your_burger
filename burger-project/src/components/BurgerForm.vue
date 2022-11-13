<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burgerForm" @submit="createBurger">
                <div class="inputContainer">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" name="nome" id="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="inputContainer">
                    <label for="pao">Escolha o Pão</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo"> {{ pao.tipo }} </option>
                    </select>
                </div>
                <div class="inputContainer">
                    <label for="carne">Escolha a Carne do seu burger</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo"> {{ carne.tipo }} </option>
                    </select>
                </div>
                <div class="inputContainer" id="opcionaisContainer">
                    <label for="opcionais" id="opcionaisTitle">Selecione os opcionais</label>
                    <div class="checkboxContainer" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais"
                            :value="opcional.tipo">
                        <span> {{ opcional.tipo }} </span>
                    </div>
                </div>
                <div class="inputContainer">
                    <input type="submit" class="submitBtn" value="Criar meu Burger!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';

export default {
    name: "BurgerForm",
    data() {
        return {
            paes: "",
            carnes: "",
            opcionaisdata: "",
            nome: "",
            pao: "",
            carne: "",
            opcionais: [],
            msg: ""
        };
    },
    methods: {
        async getIngredients() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        async createBurger(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            };
            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });
            const res = await req.json();

            //colocar mensagem no sistema
            this.msg = `Pedido Nº ${res.id} realizado com sucesso`;

            //limpar mensagem
            setTimeout(() => this.msg = "", 3000);

            //limpar os campos após o envio
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";
        }
    },
    mounted() {
        this.getIngredients();
    },
    components: {
        Message
    }
}
</script>

<style scoped>
#burgerForm {
    max-width: 400px;
    margin: 0 auto;
}

.inputContainer {
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

#opcionaisContainer {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionaisTitle {
    width: 100%;
}

.checkboxContainer {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkboxContainer span,
.checkboxContainer input {
    width: auto;
}

.checkboxContainer span {
    margin-left: 6px;
    font-weight: bold;
}

.submitBtn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.5s;
}

.submitBtn:hover {
    background-color: transparent;
    color: #222;
}
</style>