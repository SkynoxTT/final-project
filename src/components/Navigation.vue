<template>
    <div class="container">
        <nav>
            <router-link class="col" to="/">Домашняя Страница</router-link>
            <router-link class="col" to="/chat">Чат</router-link>
            <router-link class="col" to="/test">Подгрузка API</router-link>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'NavComp'
}  
</script>

<style scoped>
.container{
    background-color: black;
    height: 70px;
    width: 100%;
    display: flex;
    justify-content: center;
}
nav{
    width: 500px;
    height: 70px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.col{
    color: white;
    text-decoration: none;
    font-weight: 900;
    font-family: Georgia, 'Times New Roman', Times, serif;
}
</style>