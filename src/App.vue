<template>
	<MainScreen v-if="selectedScreen === 'MainScreen'" />
	<GameContainer v-if="selectedScreen === 'GameContainer'" />
</template>

<script>
import GameContainer from './components/GameContainer/GameContainer.vue';
import MainScreen from './components/MainScreen/MainScreen.vue';

export default {
    components: { GameContainer, MainScreen },
	data() {
		return {
			selectedScreen: "MainScreen",
			
		}
	},
	methods: {
		setSelectedScreen(component) {
			this.selectedScreen = component
		}
	},
	provide() {
		return {
			setSelectedScreen: this.setSelectedScreen
		}
	}
};
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;700;900&display=swap');
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	body {
		font-family: 'Montserrat', sans-serif;
	}
	html, body {
		overflow-x: hidden;
	}
	.gameContainer {
		position: relative;
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
</style>
