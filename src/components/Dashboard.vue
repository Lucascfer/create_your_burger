<template>
    <div id="burgerTable">
        <Message :msg="msg" v-show="msg" />

        <div>
            <div id="burgerTableHeading">
                <div class="orderId">#:</div>
                <div>Cliente</div>
                <div>Pão</div>
                <div>Carne</div>
                <div>Opcionais</div>
                <div>Ações:</div>
            </div>
        </div>

        <div id="burgerTableRows">
            <div class="burgerTableRow" v-for="burger in burgers" :key="burger.id">
                <div class="orderNumber"> {{ burger.id }} </div>
                <div> {{ burger.nome }} </div>
                <div> {{ burger.pao }} </div>
                <div> {{ burger.carne }} </div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in burger.opcionais" :key="index"> {{ opcional }} </li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                        <option value="">Selecione</option>
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo"> {{
                                s.tipo
                        }} </option>
                    </select>
                    <button class="deleteBtn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';

export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burgerId: null,
            status: [],
            msg: null
        }
    },

    components: {
        Message
    },

    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3000/burgers");

            const data = await req.json();

            this.burgers = data;

            // resgatar os status
            this.getStatus();
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;
        },
        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            //colocar mensagem no sistema
            this.msg = `Pedido removido com sucesso!`;

            //limpar mensagem
            setTimeout(() => this.msg = "", 3000);

            this.getPedidos();
        },
        //atualização do status
        async updateBurger(event, id) {
            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            //colocar mensagem no sistema
            this.msg = `O pedido Nº ${res.id} foi atualizado para ${res.status}`;

            //limpar mensagem
            setTimeout(() => this.msg = "", 3000);
        }
    },
    mounted() {
        this.getPedidos();
    }
}
</script>

<style scoped>
#burgerTable {
    max-width: 1200px;
    margin: 0 auto;
}

#burgerTableHeading,
#burgerTableRows,
.burgerTableRow {
    display: flex;
    flex-wrap: wrap;
}

#burgerTableHeading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

#burgerTableHeading div,
.burgerTableRow div {
    width: 19%;
}

.burgerTableRow {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
}

#burgerTableHeading .orderId,
.burgerTableRow .orderNumber {
    width: 5%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.deleteBtn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.5s;
}

.deleteBtn:hover {
    background-color: transparent;
    color: #222;
}
</style>