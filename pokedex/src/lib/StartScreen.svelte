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
<p>Highscore: {highscore}</p>
<button on:click={startGame}>Start</button>
