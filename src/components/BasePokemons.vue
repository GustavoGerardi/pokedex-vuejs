<template>

    <div class="container">
        <p>Pokemons Primeira Geração</p>
        <div class="pesquisa">
            <input v-model="pokemonFiltered" type="text" placeholder="Digite o nome do pokemon">
        </div>
    </div>

    <div class="listaPokemons">
        <div class="cardPoke" v-for="pokemon in filterPokemon" :key="pokemon.name">
            <div class="infos">
                <p>
                    {{capitalizeFirstLetter(pokemon.name)}}
                </p>
            </div>
            <div class="imag">
                <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getIdPokemon(pokemon)}.png`" :alt=pokemon.name>
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
            pokemons: [],
            pokemonFiltered: ""
        }
    },
    methods: {
        capitalizeFirstLetter(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        },
        getIdPokemon(pokemon){
            return pokemon.url.split("/")[6]
        }
    },
    computed: {
        filterPokemon() {
            return this.pokemons.filter(poke => {
                return poke.name.includes(this.pokemonFiltered)
            })
        }
    }
}

</script>

<style scoped lang="scss">

    $bgcolor: rgb(237, 243, 249);

    body {
    margin: 0;
    padding: 0;
    }

    .listaPokemons{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    
    .cardPoke {
        margin: 2px;
        width: 180px;
        height: 120px;
        background-color: $bgcolor;
    }

    .infos > p{
        margin: 0;
    }

    .cardPoke:hover{
        background-color: darken($color: $bgcolor, $amount: 10%);
    }

    .container {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 10px;

        p{
            font-weight: bolder;
            margin-right: 50px;
        }
    }
</style>