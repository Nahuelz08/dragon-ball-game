<template>
	<GameOver
		v-if="
			gameWinner === 'Enemy' ||
			gameWinner === 'Player' ||
			gameWinner === 'Draw'
		"
		@play-again="startGame"
		:whoWon="gameWinner"
	/>
	<div class="gameContainer" v-else>
		<TheArena />
		<GohanPlayer
			:player-life="playerLife"
			:playerKiNumber="playerKi"
			:player-action="playerAction"
		/>
		<CellEnemy
			:enemy-life="enemyLife"
			:enemyKiNumber="enemyKi"
			:enemy-action="enemyAction"
		/>
		<ButtonsControl
			@player-attack="playerAttacks"
			@player-special="playerSpecialAttack"
			@player-charge="playerCharges"
			@player-surrender="playerSurrendered"
			:playerHasKi="playerKi"
			:canUse="actions"
		/>
	</div>
</template>

<script>
import TheArena from "../TheArena/TheArena.vue";
import GohanPlayer from "../GohanPlayer/GohanPlayer.vue";
import CellEnemy from "../CellEnemy/CellEnemy.vue";
import ButtonsControl from "../ButtonsControl/ButtonsControl.vue";
import GameOver from "../GameOver/GameOver.vue";

function getRandomValue(min, max) {
	return Math.floor(Math.random() * (max - min)) + min;
}

export default {
	data() {
		return {
			playerLife: 100,
			enemyLife: 100,
			playerKi: 100,
			enemyKi: 100,
			gameWinner: "",
			playerAction: "gohanStand",
			enemyAction: "cellStand",
			actions: true,
		};
	},
	components: { TheArena, GohanPlayer, CellEnemy, ButtonsControl, GameOver },
	methods: {
		startGame() {
			this.playerLife = 100;
			this.enemyLife = 100;
			this.playerKi = 100;
			this.enemyKi = 100;
			this.gameWinner = "";
			(this.playerAction = "gohanStand"),
				(this.enemyAction = "cellStand"),
				(this.actions = true);
		},
		playerAttacks() {
			this.playerAction = "gohanAttack";
			this.actions = false;
			const attackDmg = getRandomValue(7, 12);
			this.enemyLife = this.enemyLife - attackDmg;
			console.log("enemy life: " + this.enemyLife);
			const playerKiCharge = attackDmg * 3;
			if (this.playerKi + playerKiCharge > 100) {
				console.log("exceso");
				this.playerKi = 100;
			} else {
				this.playerKi += playerKiCharge;
			}
			this.enemyActions();
			setTimeout(() => {
				this.playerAction = "gohanStand";
				this.actions = true;
			}, 400);
		},
		playerSpecialAttack() {
			this.playerAction = "gohanSpecial";
			this.actions = false;
			if (this.playerKi === 100) {
				const specialAttackDmg = getRandomValue(13, 20);
				this.enemyLife = this.enemyLife - specialAttackDmg;
				this.playerKi = 0;
				this.enemyActions();
				setTimeout(() => {
					this.playerAction = "gohanStand";
					this.actions = true;
				}, 650);
			} else {
				return;
			}
		},
		playerCharges() {
			this.playerAction = "gohanCharge";
			this.actions = false;
			const kiCharge = 75;
			const playerHeals = getRandomValue(2, 4);
			if (this.playerKi + kiCharge > 100) {
				console.log("exceso");
				this.playerKi = 100;
			} else {
				this.playerKi += kiCharge;
			}
			if (this.playerLife + playerHeals > 100) {
				this.playerLife = 100;
			} else {
				this.playerLife += playerHeals;
			}
			this.enemyActions();
			setTimeout(() => {
				this.playerAction = "gohanStand";
				this.actions = true;
			}, 500);
		},
		playerSurrendered() {
			this.playerLife = 0;
		},
		enemyActions() {
			const enemyActionType = getRandomValue(1, 4);
			console.log(enemyActionType);
			if (enemyActionType === 2 && this.enemyKi === 100) {
				// Special Attack
				this.enemyAction = "cellSpecial";
				const enemySpecialAttackDmg = getRandomValue(15, 22);
				this.playerLife = this.playerLife - enemySpecialAttackDmg;
				console.log("special attack - player life: " + this.playerLife);
				this.enemyKi = 0;
				setTimeout(() => {
					this.enemyAction = "cellStand";
				}, 650);
			} else if (enemyActionType === 3) {
				// Enemy Charges
				this.enemyAction = "cellCharge";
				const kiCharge = 75;
				const enemyHeals = getRandomValue(4, 7);
				if (this.enemyKi + kiCharge > 100) {
					console.log("exceso");
					this.enemyKi = 100;
				} else {
					this.enemyKi += kiCharge;
				}
				if (this.enemyLife + enemyHeals > 100) {
					this.enemyLife = 100;
				} else {
					this.enemyLife += enemyHeals;
				}
				setTimeout(() => {
					this.enemyAction = "cellStand";
				}, 550);
				console.log("enemy charge");
			} else {
				// Normal Attack
				this.enemyAction = "cellAttack";
				const enemyAttackDmg = getRandomValue(8, 13);
				this.playerLife = this.playerLife - enemyAttackDmg;
				console.log("normal attack - player life: " + this.playerLife);
				const enemyKiCharge = enemyAttackDmg * 2;
				if (this.enemyKi + enemyKiCharge > 100) {
					console.log("exceso");
					this.enemyKi = 100;
				} else {
					this.enemyKi += enemyKiCharge;
				}
				setTimeout(() => {
					this.enemyAction = "cellStand";
				}, 400);
				console.log(this.enemyKi);
			}
		},
	},
	watch: {
		playerLife(value) {
            setTimeout(() => {
                if (value <= 0 && this.enemyLife <= 0) {
                    this.actions = false
                    this.enemyAction = "cellEnd";
                    this.playerAction = "gohanEnd";
                    setTimeout(() => {
                        this.gameWinner = "Draw";
                    }, 1245);
                } else if (value <= 0) {
                    this.actions = false
                    this.playerAction = "gohanEnd";
                    setTimeout(() => {
                        this.gameWinner = "Enemy";
                    }, 1245);
                }
            }, 650);
		},
		enemyLife(value) {
            setTimeout(() => {
                
                if (value <= 0 && this.playerLife <= 0) {
                    this.actions = false
                    this.enemyAction = "cellEnd";
                    this.playerAction = "gohanEnd";
                    setTimeout(() => {
                        this.gameWinner = "Draw";
                    }, 1245);
                } else if (value <= 0) {
                    this.actions = false
                    this.enemyAction = "cellEnd";
                    setTimeout(() => {
                        this.gameWinner = "Player";
                    }, 1245);
                }
            }, 650);
		},
	},
};
</script>

<style scoped>
.gameContainer {
	position: relative;
}
</style>
