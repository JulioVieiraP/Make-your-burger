<script setup>
import { onMounted, reactive } from 'vue';

const obj = reactive({
    burgers: null,
    burger_id: null,
    status: [],
})

const getPedidos = async () =>{
    const req = await fetch('http://localhost:3000/burgers')
    const data = await req.json()
    
    obj.burgers = data

    getStatus()
}

const getStatus = async () => {
    const req = await fetch('http://localhost:3000/status')
    const data = await req.json()

    obj.status = data
}
 

onMounted(getPedidos)
</script>
<template>
    <table class="burger-table">
        <thead>
            <tr class="burger-table-heading">
                <th class="order-id">#:</th>
                <th>Cliente:</th>
                <th>Pão:</th>
                <th>Carne:</th>
                <th>Opcionais:</th>
                <th>Ações:</th>
            </tr>
        </thead>
        <tbody class="burger-table-rows">
            <tr class="burger-table-row" v-for="burger in obj.burgers" :key="burger.id">
                <td class="order-number">{{ burger.id }}</td>
                <td>{{ burger.nome }}</td>
                <td>{{ burger.pao }}</td>
                <td>{{ burger.carne }}</td>
                <td class="burger__list">
                    <ul v-for="(opcional, index) in burger.opcionais" :key="index">
                        <li>{{ opcional }}</li>
                    </ul>
                </td>
                <td>
                    <select name="status" class="status">
                        <option value="">Selecionada</option>
                        <option value="" v-for="status in obj.status" :key="status.id" :selected="burger.status == status.tipo">
                            {{ status.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn">Cancelar</button>
                </td>
            </tr>
        </tbody>
    </table>
    
</template>

<style scoped>
.burger-table {
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;
}

.burger-table-heading,
.burger-table-rows,
.burger-table-row {
    display: flex;
    flex-wrap: wrap;
}

.burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

.burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
}

.burger-table-heading th,
.burger-table-row td {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 19%;
}

.burger__list{
    display: flex;
    flex-direction: column;
}

.burger-table-heading .order-id,
.burger-table-row .order-number {
    width: 5%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.delete-btn {
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

.delete-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>