<script>
import PokemonCard from "./PokemonCard.svelte";
import LoadingScreen from "./LoadingScreen.svelte";

let score = 0;
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
        console.log(pokemon.length);
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

function guessYes(){
    console.log(firstPokemon());
    score++;
    if (firstPokemon().heigth >= secondPokemon().height) {
        score++;
    }
    loadNext();
}
function guessNo(){
    if (firstPokemon().heigth <= secondPokemon().height) {
        score++;
    }
    loadNext();
}

</script>
<p>Score: {score}</p>
<div id="cards">
    
    {#key score}
        {#await firstPokemon()}
            <LoadingScreen></LoadingScreen>
        {:then pokemon1}
            {#await secondPokemon()}
            <LoadingScreen></LoadingScreen>
            {:then pokemon2}
                Is
                <PokemonCard pokemon={pokemon1}></PokemonCard>
                taller than
                <PokemonCard pokemon={pokemon2}></PokemonCard>?
                <button on:click={guessYes}>Yes</button>
                <button on:click={guessNo}>No</button>
            {:catch error}
                Error loading pokemon api
            {/await}
        {:catch error}
            Error loading pokemon api
        {/await}
        
    {/key}
    
</div>
