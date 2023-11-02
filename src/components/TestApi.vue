<template>
    <div class="cont">
        <div class="h">NBA Teams</div>
        <div v-if="isLoad">Загрузка данных...</div>
        <div v-else class="teams">
            <div v-for='(el, i) in teamData' :key='el.id' class="cont2">
                <div class="item">
                    {{i + 1}}. {{el.abbreviation}} {{el.city}} " " {{ el.full_name }}
                </div>
                <img src="https://avatars.mds.yandex.net/i?id=458ef443ed3c3779ed55a47175b8ab67bd205f00-10115290-images-thumbs&n=13" style="width:19px; height:19px" @click="removeTeam(el.id)"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TestApi',
    data(){
        return{
            teamData: [],
            isLoad: true
        }
    },

    mounted(){
        const url = 'https://free-nba.p.rapidapi.com/teams?page=0';
        const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '6aa01e9aecmsh0cdc3c233c971dbp13301djsn515058e82140',
		'X-RapidAPI-Host': 'free-nba.p.rapidapi.com'
	}
};
    

fetch(url, options)
.then(res => res.json())
.then(res => {
    this.teamData = res.data
    this.isLoad = false
})
    },

    methods: {
        removeTeam(id){
            this.teamData = this.teamData.filter((el) => el.id !== id)
        }
    }
}  
</script>

<style scoped>
.teams{
    border: 3px solid black;
    padding: 5px;
    font-size: 10px;
    background-color: white;
    border-radius: 5px;
    width: 450px;
}

.cont{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.h{
    font-weight: 900;
    color: black;
    font-size: 24px;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.cont2{
    display: flex;
    justify-content: space-between;
}

.item{
    padding-top: 10px;
}
</style>