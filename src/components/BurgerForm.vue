<script setup>
import { reactive, onMounted } from "vue";


const obj = reactive({
    paes: null,
    carnes: null,
    opcionaisdata: null,
    nome: null,
    pao: null,
    carne: null,
    opcionais: [],
    status: "Solicitado",
    msg: null,
})

const getIngredientes = async () =>{
    const req = await fetch('http://localhost:3000/ingredientes')
    const Data = await req.json()
    
    obj.paes = Data.paes
    obj.carnes = Data.carnes
    obj.opcionaisdata = Data.opcionais
}

onMounted(getIngredientes)
</script>

<template>
    <div>
        <p>componente de msg</p>
        <form class="burger__form" @submit.prevent="">
            <div class="input__container">
                <label for="nome">Nome do cliente:</label>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="input__container">
                <label for="pao">Escolha o pão do seu Burger:</label>
                <select id="pao" name="pao" v-model="obj.pao">
                    <option value="">Selecione o seu pão</option>
                    <option v-for="pao in obj.paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
                </select>
            </div>
            <div class="input__container">
                <label for="carne">Escolha a carne do seu Burger:</label>
                <select id="carne" name="carne" v-model="obj.carne">
                    <option value="">Selecione o tipo de carne</option>
                    <option v-for="carne in obj.carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                </select>
            </div>
            <div id="opcionais__container" class="input__container">
                <label for="opcionais" class="opcionais__title">Selecione os opcionais:</label>
                <div class="checkbox__container" v-for="opcional in obj.opcionaisdata" :key="opcional.id">
                    <input type="checkbox" name="opcionais" v-model="obj.opcionaisdata" :value="opcional.tipo">
                    <span>{{opcional.tipo}}</span>
                </div>
            </div>
            <div class="input__container">
                <input type="submit" class="submit-btn" value="Criar meu Burger!">
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