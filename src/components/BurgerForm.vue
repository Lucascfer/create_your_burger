<template>
    <div>
        <p>Componente de mensagem</p>
        <div>
            <form id="burgerForm">
                <div class="inputContainer">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" name="nome" id="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="inputContainer">
                    <label for="pao">Escolha o Pão</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option value="integral">Integral</option>
                    </select>
                </div>
                <div class="inputContainer">
                    <label for="carne">Escolha a Carne do seu burger</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option value="maminha">Maminha</option>
                    </select>
                </div>
                <div class="inputContainer" id="opcionaisContainer">
                    <label for="opcionais" id="opcionaisTitle">Selecione os opcionais</label>
                    <div class="checkboxContainer">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" value="salame">
                        <span>Salame</span>
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
export default {
    name: "BurgerForm"
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