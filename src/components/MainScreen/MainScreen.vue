<template>
    <div class="mainContainer">
        <h1>Welcome to Dragon Ball!</h1>
        <button @click="setSelectedScreen('GameContainer')">Start Game</button>
        <h3>Created by <a href="https://github.com/Nahuelz08" target="_blank">Nahuel Gramajo</a></h3>
    </div>
</template>

<script>
export default {
    inject: ['setSelectedScreen']
}
</script>

<style>
.mainContainer {
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
/* Media Query Mobile */
@media only screen and (min-width:0px) and (max-width: 480px){
    .mainContainer {
        text-align: center;
    }
}
</style>