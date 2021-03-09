<template>
  <div id="app" class="column is-half is-offset-one-quarter">
    <img src ="./assets/pokemon-logo.png" id="logo"/>
    <h4 class="is-size-4">Pokedex</h4>
    <input class="input is-rounded" type="text" placeholder="Find pokemon with name" v-model="finded"/>
    <button class="button is-fullwidth is-link" id="findBtn" @click="find">Finder</button>
    <div> 
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
        </div>
    </div>

   
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/pokemon'
  export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons:[],
      finded:''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components:{
    Pokemon
  },
  methods:{
    find: function(){
      this.filteredPokemons = this.pokemons
      if(this.finded == '' || this.finded == ' '){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.indexOf(this.finded.toLowerCase()) != -1);
      }
    }
  },
  computed:{
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
#findBtn{
  margin-top: 10px;
}

</style>
