<template>
    <div v-if="userName" class="cont">
        <div class="chat">
            <h2>Чат</h2>

            <div class="text" v-for="msg in messages" :key="msg.id">
               {{ msg.user }}: {{ msg.text }}
            </div>

            <div v-show="emptyMsg" class="empty">Текущих сообщений нет</div>
        </div>

        <div class="functions">
                <input v-model="newMessage" placeholder="Введите сообщение" class="inp"/>
                <button @click="sendMessage" class="bttn">Отправить</button>
                <button @click="delMessage" class="bttn2">Удалить</button>
        </div>
    </div>

    <div v-else class="alert">
        Для авторизации перейдите по <router-link :to="{name: 'Home'}">ссылке</router-link>
    </div>
</template>

<script>
export default {
    name: 'ChatPage',
    data(){
        return {
            messages: [],
            newMessage: '',
            emptyMsg: true,
            userName: localStorage.getItem('userName'),
        }
    },

    computed(){
        localStorage.setItem('userName', this.$route.query.userName)
    },

    methods: {
        sendMessage(){
            if(this.newMessage !== ''){
                this.emptyMsg = false
                this.messages.push({id: new Date().getTime(), text: this.newMessage, user: this.userName})
                this.saveChatRecords()
                this.newMessage = ''
            }
        },

        saveChatRecords(){
            const records = this.messages
            localStorage.setItem(`messages_${this.userName}`, JSON.stringify(records))
        },

        delMessage(){
            this.messages = []
            localStorage.removeItem(`messages_${this.userName}`, JSON.stringify(this.messages))

            this.emptyMsg = true
        },

        loadChatRecords(){
            const records = JSON.parse(localStorage.getItem(`messages_${this.userName}`))
            if(records){
                this.messages = records
                this.emptyMsg = false
            }
        }
    },

    created(){
        this.loadChatRecords()
    }
}  
</script>

<style scoped>
h2{
    color: gray;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.text{
    margin-bottom: 10px;
    margin-left: 20px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.chat{
    margin-bottom: 20px;
    width: 300px;
    height: 100%;
    border: 3px solid black;
    color: black;
    background-color: white;
    font-weight: 18px;
    font-weight: bold;
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 5px;
    border-radius: 10px;
}


.empty{
    margin-bottom: 25px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.alert{
    font-family: Georgia, 'Times New Roman', Times, serif;
    color: white;
    margin-top: 300px
}

.functions{
    background-color: white;
    padding: 20px 20px 20px 20px;
    border-radius: 10px;
    border: 3px solid black;
    display: flex;
    justify-content: space-between;
}

.cont{
    display: flex;
    align-items: center;
    flex-direction: column;
}

.inp{
    margin-right: 70px;
    padding: 7px 20px 7px 7px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.bttn{
    background-color: black;
    color: white;
    transition: 0.5s;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin-right: 5px;
}

.bttn:hover{
    background-color: white;
    color: black;
    cursor: pointer;
    transition: 0.5s;
}

.bttn2{
    background-color: black;
    color: white;
    transition: 0.5s;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin-right: 5px;
}

.bttn2:hover{
    background-color: #FF5353;
    cursor: pointer;
    transition: 0.5s;
}
</style>