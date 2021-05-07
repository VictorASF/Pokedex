<template>
  <div id="app">
    <div class='column is-half is-offset-one-quarter'>
      <h4 class='is-size-4'>Pokedex</h4>
      <input class = 'input is-rounded' id='distant-top' 
             type="text" placeholder="Buscar pokemon pelo nome" v-model='busca'>
      <button class='button is-fullwidth is-success is-rounded' id='distant-top'>Buscar</button>
      <div v-for="(poke,index) in resultadoBusca" :key='index'>
          <Pokemon :name="poke.name" :url ="poke.url" :id="index"/>      
      </div>
    </div>
  
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      busca: ""
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(
      res=>{
        this.pokemons = res.data.results;
      }
    )
  },
  components:{
    Pokemon,
  },
  computed:{
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#distant-top{
  margin-top:2%;
}
</style>
