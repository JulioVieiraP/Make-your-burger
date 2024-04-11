<script setup>
const props = defineProps(['logo', 'alt'])
</script>

<template>
    <div>
        <nav class="nav">
            <RouterLink class="logo" to="/">
                <img class="logo__img" :src="logo" :alt="alt">
            </RouterLink>
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/pedidos">Pedidos</RouterLink>
        </nav>
    </div>
</template>

<style scoped>
.nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

.nav .logo {
    margin: auto;
    margin-left: 0;
}

.logo__img {
    width: 40px;
    height: 40px;
}

.nav a {
    color: #fcba03;
    margin: 12px;
    transition: .5s;
}

.nav a:hover{
    color: #fff;
}
</style>