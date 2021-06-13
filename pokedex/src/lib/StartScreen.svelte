<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    function startGame() {
		dispatch('startGame');
	}
</script>
<h1>Pokémon height game</h1>
<button on:click={startGame}>Start</button>
