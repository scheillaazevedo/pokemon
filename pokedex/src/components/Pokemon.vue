<template>
    <div class="card mt-4" :class="[infoPokemon.type == 'fire' ? 'colorFire' : '',infoPokemon.type == 'grass' ? 'colorGrass' : '', infoPokemon.type == 'water' ? 'typeWater' : '', infoPokemon.type == 'bug' ? 'typeBug' : '', infoPokemon.type == 'normal' ? 'colorNormal' : '', infoPokemon.type == 'poison' ? 'colorPoison' : '', infoPokemon.type == 'electric' ? 'colorElectric' : '', infoPokemon.type == 'ground' ? 'colorGround' : '',]">
    <img :src="infoPokemon.img" class="card-img-top" alt="...">
    <div class="card-body">
        <h4 class="card-title">{{name | titleUpper }}</h4>
        <div class="d-flex justify-content-between mt-3">
            <p class="card-text">ID: {{numId}}</p>
            <div>
                <span :class="[infoPokemon.type == 'fire' ? 'typeFire' : '',infoPokemon.type == 'grass' ? 'typeGrass' : '', infoPokemon.type == 'water' ? 'typeWater' : '', infoPokemon.type == 'bug' ? 'typeBug' : '', infoPokemon.type == 'normal' ? 'typeNormal' : '', infoPokemon.type == 'poison' ? 'typePoison' : '', infoPokemon.type == 'electric' ? 'typeElectric' : '', infoPokemon.type == 'ground' ? 'typeGround' : '',]">
                    {{infoPokemon.type}}</span>
            </div>
        </div>
        <div class="games mt-2 d-flex flex-column ">
            <div class="d-flex justify-content-between align-items-center">
                <h5>NOME DOS JOGOS:</h5>
                <button type="button" class="btn btn-view" @click="openGame = !openGame">{{openGame ? '-' : '+'}}</button>
            </div>
            <div class="align-items-start" v-if="openGame">
                <span v-for="(itemGame, index) in games" :key="index">{{itemGame.version.name}},</span>
            </div>
        </div>
        <div class="Locais mt-2 d-flex flex-column ">
            <div class="d-flex justify-content-between align-items-center">
                <h5>LOCAIS:</h5>
                <button type="button" class="btn btn-view" @click="openLocal = !openLocal">{{openLocal ? '-' : '+'}}</button>
            </div>
            <div class="align-items-start" v-if="openLocal">
              {{location}}
            </div>
        </div>
    
    </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
    created() {
        axios.get(this.url).then(resposta =>{
            this.infoPokemon.type = resposta.data.types[0].type.name;
            this.infoPokemon.img = resposta.data.sprites.front_default;
            this.games = resposta.data.game_indices;
            this.identificador = resposta.data.id;
            this.location = resposta.data.location_area_encounters;
        })
    },
    data(){
        return {
            openGame: false,
            openLocal: false,
            games: [],
            location: '',
            infoPokemon: {
                type: '',
                img: '',
                identificador: '',
            },
        }
    },
    props: {
        numId: Number,
        name: String,
        url: String,
        locationPoke: String,
    },
    filters:{
        titleUpper(value){
            let newTitle = value.toUpperCase()
            return newTitle
        }
    },
}
</script>