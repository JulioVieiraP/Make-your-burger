<script setup>
import { reactive, onMounted } from "vue";
import Message from "./Message.vue";
import { API_BASE_URL } from "../api/api";

const obj = reactive({
    paes: null,
    carnes: null,
    opcionaisdata: null,
    nome: null,
    pao: null,
    carne: null,
    opcionais: [],
    msg: null,
    loading: false
})

const getIngredientes = async () => {
    const req = await fetch(`${API_BASE_URL}/burgers/ingredientes/`)
    const Data = await req.json()

    obj.paes = Data.paes
    obj.carnes = Data.carnes
    obj.opcionaisdata = Data.opcionais
}

const createBurger = async () => {
    obj.loading = true; // Desativa inputs
    const data = {
        nome: obj.nome,
        carne: obj.carne,
        pao: obj.pao,
        opcionais: obj.opcionais,
        status: "Solicitado"
    }

    const dataJson = JSON.stringify(data)
    console.log(dataJson)

    try {
        const req = await fetch(`${API_BASE_URL}/burgers/`, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: dataJson
        });

        const res = await req.json()

        obj.msg = "Pedido realizado com sucesso"

        obj.nome = ''
        obj.pao = ''
        obj.carne = ''
        obj.opcionais = []

        setTimeout(() => {
            obj.msg = null
        }, 5000);

    } catch (error) {
        console.error("Erro ao enviar o pedido:", error);
        obj.msg = "Ocorreu um erro ao enviar o pedido.";
    } finally {
        obj.loading = false;
    }
}


onMounted(getIngredientes)
</script>

<template>
    <div>
        <Message :msg = 'obj.msg' v-show="obj.msg"/>
        <form class="burger__form" @submit.prevent="createBurger">
            <div class="input__container">
                <label for="nome">Nome do cliente:</label>
                <input type="text" id="nome" name="nome" v-model="obj.nome" placeholder="Digite o seu nome">
            </div>
            <div class="input__container">
                <label for="pao">Escolha o pão do seu Burger:</label>
                <select id="pao" name="pao" v-model="obj.pao">
                    <option value="">Selecione o seu pão</option>
                    <option v-for="pao in obj.paes" :key="pao.id" :value="pao.nome">{{ pao.nome }}</option>
                </select>
            </div>
            <div class="input__container">
                <label for="carne">Escolha a carne do seu Burger:</label>
                <select id="carne" name="carne" v-model="obj.carne">
                    <option value="">Selecione o tipo de carne</option>
                    <option v-for="carne in obj.carnes" :key="carne.id" :value="carne.nome">{{ carne.nome }}</option>
                </select>
            </div>
            <div id="opcionais__container" class="input__container">
                <label for="opcionais" class="opcionais__title">Selecione os opcionais:</label>
                <div class="checkbox__container" v-for="opcional in obj.opcionaisdata" :key="opcional.id">
                    <input type="checkbox" name="opcionais" v-model="obj.opcionais" :value="opcional.nome">
                    <span>{{ opcional.nome }}</span>
                </div>
            </div>
            <div class="input__container">
                <input type="submit" class="submit-btn" value="Criar meu Burger!" :disabled="obj.loading">
            </div>

        </form>
    </div>
</template>



<style scoped>
.burger__form {
    max-width: 400px;
    margin: 0 auto;
}

.input__container {
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
    width: 400px;
}

#opcionais__container {
    flex-direction: row;
    flex-wrap: wrap;
}

.opcionais__title {
    width: 100%;
}

.checkbox__container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox__container span,
.checkbox__container input {
    width: auto;
}

.checkbox__container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
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

.submit-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>