<script>
    export let pokemon;

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }
</script>

<div class="pokemonCard">
        <h1>{capitalizeFirstLetter(pokemon.name)}</h1>
        <img src="{pokemon.sprites.front_default}" alt="{pokemon.name}">
    
</div>