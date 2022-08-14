<template>
  <div>
    <p v-if="$fetchState.pending">Loading....</p>
    <p v-else-if="$fetchState.error">Error while fetching pokemons</p>
    <div v-else class="px-8 container mx-auto relative font-mono">
      <img src="/images/CnuhrBoNRpTPH5QpXysoFF.jpg" class="w-full h-48 object-cover">
      <div class="text-6xl font-extrabold text-color absolute top-4 right-20">pokemon</div>
      <div class="text-3xl font-bold text-white absolute top-16 right-20">details</div>

      <div class="space-y-4 p-8 bg">
        <div class="text-lg bg-contant">Name: <span>{{ pokemons.name }}</span></div>
        <div class="grid grid-cols-2 bg-contant">
          <p class="col-span-2">default</p>
          <img :src="pokemons.sprites.front_default" class="w-32 h-32"/>
          <img :src="pokemons.sprites.back_default" class="w-32 h-32"/>
        </div>
        <div class="grid grid-cols-2 bg-contant">
          <p class="col-span-2">Shiny</p>
          <img :src="pokemons.sprites.front_shiny" class="w-32 h-32"/>
          <img :src="pokemons.sprites.back_shiny" class="w-32 h-32"/>
        </div>
        <div class="bg-contant">Number: {{ pokemons.id }}</div>
        <div class="bg-contant">Types: <span v-for="(type,index) in pokemons.types" :key="index">{{type.type.name}}</span></div>
        <ol class="grid grid-cols-3 bg-contant">
          <p>Abilities:</p>
          <li v-for="(abilities,index) in pokemons.abilities" :key="index" class="list-decimal">{{ abilities.ability.name}}</li>
        </ol>
        <div class="bg-contant">Height: <span>{{pokemons.height}} cm</span></div>
        <div class="bg-contant">Weight: <span>{{ pokemons.weight }} kg</span></div>
        <ul class="grid grid-cols-2 list-inside  bg-contant">
          <p class="col-span-2">Stats:</p>
          <li v-for="(stats,index) in pokemons.stats" :key="index" class="list-disc">{{stats.stat.name}} {{stats.base_stat}}</li>
        </ul>
        <div class="grid grid-cols-2 bg-contant">
          <p>dream world</p>
          <p>home default <span>, shiny</span></p>
          <img :src="pokemons.sprites.other.dream_world.front_default" class="w-32 h-32"/>
          <div>
            <img :src="pokemons.sprites.other.home.front_default" class="w-32 h-32 inline-block"/>
            <img :src="pokemons.sprites.other.home.front_shiny" class="w-32 h-32 inline-block"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'index-page',
  data() {
    return {
      pokemons: [],
    }
  },
  async fetch() {
    this.pokemons = await fetch(
      'https://pokeapi.co/api/v2/pokemon/ditto'
    ).then(res => res.json())
  }
}
</script>

<style scoped>
.text-color{
  color: #f2b142;
}
.bg{
  background-color: #c6b3d7;
}
.bg-contant{
  background-color: white;
  padding: 10px;
  border-radius: 25px;
  border: #8a7562 solid;
}
</style>
