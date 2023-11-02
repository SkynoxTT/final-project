<template>
    <div class="container">
        <div v-if="isAuth" class="cont3">
            <div class="boberoleg">Приветствую, {{ userName }}</div>
            <button @click="logout">Выйти</button>
        </div>

        <div v-else class="cont2">
            <input v-model="userName" placeholder="Введите имя"/>
            <button @click="login">Войти</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HomePage',
    data(){
        return {
            isAuth: false,
            userName: ''
        }
    },
    methods: {
        login(){
            if(this.userName !== ''){
                this.isAuth = true
                localStorage.setItem('isAuth', true)
                localStorage.setItem('userName', this.userName)

                this.$router.push({
                    name: 'Chat',
                    query: {userName: this.userName}
                })
            } else {
                alert("Введите имя")
            }
        },

        logout(){
            this.isAuth = false
            this.userName = ''
            localStorage.removeItem('isAuth')
            localStorage.removeItem('userName')
        }
    },

    created(){
        if(localStorage.getItem('isAuth')) {
            this.isAuth = true
            this.userName = localStorage.getItem('userName')
        }
    }
}  
</script>

<style scoped>
.container{
    margin-top: 275px;
}

button{
    background-color: black;
    color: white;
    transition: 0.5s;
    padding: 7px 45px 7px 45px;
    border-radius: 15px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

button:hover{
    background-color: white;
    color: black;
    cursor: pointer;
    transition: 0.5s;
}

.cont2{
    border: 3px solid black;
    padding: 5px;
    border-radius: 5px;
    background-color: white;
    height: 100px;
    display: flex;
    align-items: center;
    flex-direction: column;
}

.cont3{
    border: 3px solid black;
    padding: 5px;
    border-radius: 5px;
    background-color: white;
    height: 60px;
    display: flex;
    align-items: center;
    flex-direction: column;
}

input{
    padding: 15px 200px 15px 15px;
    margin-bottom: 20px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.boberoleg{
    margin-bottom: 8px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}
</style>