<script>
import PokemonCard from "./PokemonCard.svelte";
import LoadingScreen from "./LoadingScreen.svelte";
import { createEventDispatcher } from 'svelte';

const dispatch = createEventDispatcher();

export let score = 0;
let pokemonOrder = [];
let pokemon = [];
for (let i = 0; i < 898; i++) {
    pokemonOrder.push(i + 1);
}
pokemonOrder = pokemonOrder
    .map((a) => ({sort: Math.random(), value: a}))
    .sort((a, b) => a.sort - b.sort)
    .map((a) => a.value);

loadNext();

function loadNext(){
    while (pokemon.length < score + 10) {
        pokemon.push((async p => {
        const res = await fetch("https://pokeapi.co/api/v2/pokemon/" + pokemonOrder[p.length]);
		const pokemon = await res.text();
		if (res.ok) {
			return JSON.parse(pokemon);
		} else {
			throw new Error(pokemon);
		}
    })(pokemon));
    }
}
function firstPokemon(){
    return pokemon[score];
}
function secondPokemon(){
    return pokemon[score + 1];
}

function guessCorrect(){
    score++;
    loadNext();
}
function guessWrong(pokemon1, pokemon2){
    if (typeof window !== 'undefined') {
        if (score > localStorage.getItem('highscore')) {
            localStorage.setItem('highscore', score);
        }
    }
    dispatch("endGame", {pokemon1, pokemon2});
}

</script>
<p>Score: {score}</p>

    
    {#key score}
        {#await firstPokemon()}
            <LoadingScreen></LoadingScreen>
        {:then pokemon1}
            {#await secondPokemon()}
            <LoadingScreen></LoadingScreen>
            {:then pokemon2}
            <div id="cards" class="row">
                <p class="column">Is</p>
                <PokemonCard pokemon={pokemon1} class="column"></PokemonCard>
                <p class="column">Taller than</p>
                <PokemonCard pokemon={pokemon2} class="column"></PokemonCard>
                <p class="column">?</p>
            </div>
            <div class="row">
                <button on:click={pokemon1.height >= pokemon2.height ? guessCorrect : (() => {guessWrong(pokemon1, pokemon2)})}>Yes</button>
                <button on:click={pokemon1.height <= pokemon2.height ? guessCorrect : (() => {guessWrong(pokemon1, pokemon2)})}>No</button>
            </div>
            {:catch error}
                Error loading pokemon api
            {/await}
        {:catch error}
            Error loading pokemon api
        {/await}
        
    {/key}
