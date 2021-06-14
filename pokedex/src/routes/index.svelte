<script>
    import StartScreen from "$lib/StartScreen.svelte";
    import GameScreen from "$lib/GameScreen.svelte";

    let state = "Start";
    function startGame() {
        state = "Game";
    }
    function endGame(){
        state = "Start"
    }
</script>

{#if state == "Start"}
    <StartScreen on:startGame={startGame}></StartScreen>
{:else if state == "Game"}
    <GameScreen on:endGame={endGame}></GameScreen>
{/if}


