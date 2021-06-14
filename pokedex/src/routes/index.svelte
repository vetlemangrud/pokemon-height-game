<script>
    import "../stylesheet.css";
    import StartScreen from "$lib/StartScreen.svelte";
    import GameScreen from "$lib/GameScreen.svelte";
    import GameOverScreen from "$lib/GameOverScreen.svelte";

    let state = "Start";
    let score = 0;
    let losingPokemon;

    function startGame() {
        score = 0;
        state = "Game";
    }
    function endGame(evt){
        losingPokemon = evt.detail;
        state = "GameOver";
    }
    function toMenu() {
        state = "Start";
    }
</script>
<header>
    <h1>Pokémon Height Game</h1>
</header>
<main>
    {#if state == "Start"}
        <StartScreen on:startGame={startGame}></StartScreen>
    {:else if state == "Game"}
        <GameScreen bind:score={score} on:endGame={endGame}></GameScreen>
    {:else if state == "GameOver"}
        <GameOverScreen score={score} losingPokemon={losingPokemon} on:back={toMenu}></GameOverScreen>
    {/if}
</main>


