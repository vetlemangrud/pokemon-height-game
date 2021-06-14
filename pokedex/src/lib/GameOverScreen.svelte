<script>
    import PokemonCard from "$lib/PokemonCard.svelte";
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    export let score = 0;
    export let losingPokemon;
    let pokemon1 = losingPokemon.pokemon1;
    let pokemon2 = losingPokemon.pokemon2;

    function back() {
        dispatch("back");
    }
</script>
<h1>Game Over</h1>
<p class="scoreCounter">Score: {score}</p>
<div id=cards>
    <PokemonCard pokemon={pokemon1} showHeight={true}></PokemonCard>
    <PokemonCard pokemon={pokemon2} showHeight={true}></PokemonCard>
</div>
<button on:click={back}>Back</button>
