<script setup>
const props = defineProps({
    msg : String
})
</script>

<template>
    <div class="message__container">
        <p>{{ msg }}</p>
    </div>
</template>

<style scoped>
.message__container{
    color: #004085;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
}
</style>