<template>
    <div class="card mt-4">
    <img :src="infoPokemon.img" class="card-img-top" alt="...">
    <div class="card-body">
        <p class="card-text">ID: {{numId}}</p>
        <h5 class="card-title">{{name | titleUpper }}</h5>
        <p class="card-text">{{url}}</p>
    </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
    created() {
        axios.get(this.url).then(resposta =>{
            this.infoPokemon.type = resposta.data.type;
            this.infoPokemon.img = resposta.data.sprites.front_default;
            console.log(resposta.data)
        })
    },
    data(){
        return {
            infoPokemon: {
                type: '',
                img: '',
            }
        }
    },
    props: {
        numId: Number,
        name: String,
        url: String  
    },
    filters:{
        titleUpper(value){
            let newTitle = value.toUpperCase()
            return newTitle
        }
    }
}
</script>