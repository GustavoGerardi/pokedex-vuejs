<template>

    <div class="listaPokemons">
        <div class="cadaPoke" v-for="(pokemon, index) in pokemons" :key="pokemon.name">
            <div class="infos">
                {{index+1}} {{capitalizeFirstLetter(pokemon.name)}}
            </div>
            <div class="imag">
                <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index+1}.png`" :alt=pokemon.name>
            </div>
        </div>
    </div>
    
</template>

<script>
import axios from 'axios' 

export default {
  mounted() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=150&offset=0').then((response) => {
        this.pokemons = response.data.results 
    })
    },
    data(){
        return {
            pokemons: []
        }
    },
    methods: {
        capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
        }
    }
}

</script>

<style>

    .listaPokemons{
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
    }
    
    .cadaPoke {
        display: flex;
        background-color: rgba(109, 94, 94, 0.192);
        padding: 10px;
        margin: 10px;
        border: solid 5px black;
        width: 200px;
        height: 100px;
        background-color: white;
    }

    .infos{
        display: block;
        text-align: center;
        width: 200px;
        height: 50px;
        padding: 3px;
        border: solid 1px;
    }

    
    .cadaPoke .imag{
        display: block;
        justify-content: center;
        text-align: center;
        width: 200px;
        border: solid;
    }

</style>