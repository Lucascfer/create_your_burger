<template>
    <div id="burgerTable">
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
            <div class="burgerTableRow">
                <div class="orderNumber">1</div>
                <div>João</div>
                <div>Pao</div>
                <div>Carne</div>
                <div>
                    <ul>
                        <li>Opcional</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status">
                        <option value="">Selecione</option>
                    </select>
                    <button class="deleteBtn">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard"
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