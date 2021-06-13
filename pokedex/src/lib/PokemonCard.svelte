<script>
    export let num;

    let pokemonPromise = (async () => {
        const res = await fetch("https://pokeapi.co/api/v2/pokemon/" + num);
		const pokemon = await res.text();

		if (res.ok) {
			return JSON.parse(pokemon);
		} else {
			throw new Error(pokemon);
		}
    })()

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }
</script>

<div class="pokemonCard">
    {#await pokemonPromise}
        <p>Loading Pokémon...</p>
    {:then pokemon}
        <h1>{capitalizeFirstLetter(pokemon.name)}</h1>
        <img src="{pokemon.sprites.front_default}" alt="">
    {:catch error}
        <p>Error loading pokemon :(</p>
    {/await}
    
</div>