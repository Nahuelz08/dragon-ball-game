<template>
    <div class="buttonsContainer">
        <button @click="$emit('player-attack')" :disabled="canUse === false" >Attack</button>
        <button @click="$emit('player-special')" :disabled="playerHasKi !== 100 || canUse === false" >Special</button>
        <button @click="$emit('player-charge')" :disabled="canUse === false" >Charge</button>
        <button @click="$emit('player-surrender')" :disabled="canUse === false" >Surrender</button>
    </div>
</template>

<script>
export default {
    emits: ['player-attack', 'player-special', 'player-charge', 'player-surrender' ],
    props: ['playerHasKi', 'canUse'],
}
</script>

<style scoped>
.buttonsContainer {
    min-height: 25vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    background-color: black;
}
button {
    width: 150px;
    height: 50px;
    font-size: 1.5rem;
    color: white;
    background-color: rgb(180, 149, 12);
    border: 2px solid rgb(112, 93, 8);
    border-radius: 1rem;
    box-shadow: 2px 2px 10px rgba(255, 255, 255, 0.35);
}
button:hover {
    cursor: pointer;
    background-color: rgb(233, 193, 14);
}
button:disabled {
    background-color: gray;
    border: 2px solid rgb(39, 39, 39);
    box-shadow: none;
    color: rgb(49, 49, 49);
}
button:disabled:hover {
    cursor:not-allowed;
}

/* Media Query Mobile */
@media only screen and (min-width:0px) and (max-width: 480px){
.buttonsContainer {
    gap: 1rem;
    flex-wrap: wrap;
}
button{
    font-size: 1rem;
    flex-basis: 150px;
}
}
</style>