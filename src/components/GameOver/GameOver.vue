<template>
    <div class="gameOverContainer">
        <h1>Game over!</h1>
        <h2 v-if="whoWon === 'Draw'">Draw Game!</h2>
        <h2 v-else>The winner is: <span :style="setWinnerColor">{{whoWon}}</span>!</h2>
        <button @click="$emit('play-again')">Play again</button>
        <h3>Created by <a href="https://github.com/Nahuelz08" target="_blank">Nahuel Gramajo</a></h3>
    </div>
</template>

<script>
export default {
    emits: ['play-again'],
    props: ['whoWon'],
    computed: {
        setWinnerColor() {
            if (this.whoWon === 'Player') {
                return { color: 'green' }
            } else if (this.whoWon === 'Enemy') {
                return { color: 'red' }
            } else {
                return { color: 'white'}
            }
        }
    }
}
</script>

<style scoped>
.gameOverContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    gap: 2rem;
    background-color: rgb(45,45,45);
    color: white;
}
a { 
    color: rgb(180, 149, 12);;
}
a:visited {
    color: gray;
}
</style>