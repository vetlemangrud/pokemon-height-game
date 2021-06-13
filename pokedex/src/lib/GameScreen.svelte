<script>
import PokemonCard from "./PokemonCard.svelte";
let score = 0;
let pokemon = [];
function initialize() {
    for (let i = 0; i < 898; i++) {
        pokemon.push(i + 1);g
    }
    pokemon = pokemon
        .map((a) => ({sort: Math.random(), value: a}))
        .sort((a, b) => a.sort - b.sort)
        .map((a) => a.value);
}
initialize();

</script>
<p>Score: {score}</p>
<div id="cards">
    Is
    <PokemonCard num={pokemon[0]}></PokemonCard>
    taller than
    <PokemonCard num={pokemon[1]}></PokemonCard>?
</div>