<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
    let highscore = 0;

    if (typeof window !== 'undefined') {
        highscore = localStorage.getItem("highscore") || 0;
    }

    function startGame() {
		dispatch('startGame');
	}
</script>
<p class="scoreCounter">Highscore: {highscore}</p>
<h2>Little Pokémon-game to play with Svelte and learn a little bit about asyncronous JavaScript (With the <a href="https://pokeapi.co/">PokéAPI</a>). CSS was obviously not the focus. Enjoy!</h2>
<button on:click={startGame}>Start</button>
