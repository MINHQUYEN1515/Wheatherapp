<template>
    <div class="wheatherapp">
        <div class="search">
            <input type="text" v-model="value" @keyup.enter="getid">
            <button @click='getid'>Search</button>
        </div>
        <div class="bodyapp">
            <h3 class='city'>{{ wheather.city }} </h3>
            <p class='day'>{{ wheather.day }}</p>
            <h1 class='nhietdo'>{{ wheather.temperature }}°C</h1>
            <img :src= "wheather.info" :alt=" wheather.mota" class='info'>
            <p class='mota'>{{ wheather.mota }}</p>
            <p class='humitidy'>Humitidy:{{ wheather.humidity }}%</p>
            <p class='presure'>Presure:{{ wheather.presure }}Pha</p>
        </div>
    </div>
</template>
<script>
import { onUpdated } from 'vue'

    const API_KEY='b565caab2fed4c9b9ca144520231107'
    const API=`http://api.weatherapi.com/v1/current.json?key=${API_KEY}&q=`
    const formmatdate=Intl.DateTimeFormat('vi-VN',
    {
        dateStyle:'full'
    }
    ) 

export default {
        data(){
            return{
                 value:'',
                 wheather:{
                    city:'--',
                    day:'--',
                    temperature:'--',
                    info:'--',
                    mota:'',
                    humidity:'--',
                    presure:'--',
                    isActicveWheather:false
                 }
            }
        },
        methods:{
            getid(){
                 fetch(API+this.value).then(reponse=>reponse.json())
                .then( data=>{
                    this.isActicveWheather=true
                    this.wheather.city=data.location.name
                    this.wheather.day=formmatdate.format(new Date(data.location.localtime))
                    this.wheather.temperature=data.current.temp_c
                    this.wheather.info=data.current.condition.icon
                    this.wheather.mota=data.current.condition.text
                    this.wheather.humidity=data.current.humidity
                    this.wheather.presure=data.current.pressure_mb      
                })
            }
        },
        mounted(){
            fetch(API).then(reponse=>reponse.json())
            .then(data=>console.log(data))
        }
        
}
</script>
<style scoped>

    .wheatherapp{
        color: #fff;
        background-color: #282c34;
        border: 1px solid black;
        width: 300px;
        height: 500px;
        margin-left: 500px;

    }
    .search{
        margin-top: 10px;
        display: flex;
        justify-content: space-evenly;
    }
    .search>input{
        border-radius: 10px;
        border: 1px solid #ccc;
        padding: 10px;
        font-size: 16px;
        border-radius: 20px;
        box-shadow: 0px 0px 5px #ccc;
        transition: box-shadow 0.3s;

    }
    .search>input:focus {
        outline: none;
        box-shadow: 0px 0px 5px #2196F3;
}
    .search>button{
          background-color: #337ab7;
            color: white;
            border: none;
            transition: background-color 0.3s ease;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        border-radius: 20px;
    }
    .search>button:hover {
        background-color: #135994;
        }
    .bodyapp{
        border-radius: 10px;
        box-shadow: 0 0 10px 2px #007FFF;
        background-color: #111111;
        margin-top: 50px;
        width: 280px;
        margin-left: 10px;
        box-sizing: border-box;
        text-align: center;
    }
    .bodyapp>img{
        height: 100px;
        width: 100px;
    }
</style>