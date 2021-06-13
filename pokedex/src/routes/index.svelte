<script>
    import StartScreen from "$lib/StartScreen.svelte";
    import GameScreen from "$lib/GameScreen.svelte";

    let state = "Start";
    function startGame() {
        state = "Game";
    }
</script>

{#if state == "Start"}
    <StartScreen on:startGame={startGame}></StartScreen>
{:else if state == "Game"}
    <GameScreen></GameScreen>
{/if}


