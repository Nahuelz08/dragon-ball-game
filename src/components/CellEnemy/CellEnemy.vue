<template>
	<div>
		<div class="cellIcon">
			<div class="lifeBarContainer">
				<p>CELL</p>
				<div class="lifeBar" :style="setEnemyLife"></div>
			</div>
			<img src="./../../assets/img/cell/cell-icon.webp" :style="enemyDefeated" alt="" />
		</div>
		<div class="kiContainer">
			<div class="kiBarContainer">
				<div class="kiBar" :style="setEnemyKiNumber"></div>
				<p class="ki">Ki: {{ enemyKiNumber }}%</p>
			</div>
		</div>
		<i :class="'cell ' + enemyAction"></i>
	</div>
</template>

<script>
export default {
	data() {
		return {};
	},
	props: ["enemy-life", "enemyKiNumber", "enemy-action"],
	computed: {
		setEnemyLife() {
			if (this.enemyLife <= 0) {
				return { width: "0%", backgroundColor: 'red' };
			} else {
				return { width: this.enemyLife + "%" };
			}
		},
		setEnemyKiNumber() {
			if (this.enemyKiNumber <= 0) {
				return { width: "0%" };
			} else {
				return { width: this.enemyKiNumber + "%" };
			}
		},
        enemyDefeated() {
            if (this.enemyLife <= 0) {
                return { filter: 'grayscale(1)' }
            } else {
                return { filter: 'grayscale(0)'}
            }
        }
	},
};
</script>

<style scoped>
.cellIcon {
	position: absolute;
	top: 0;
	right: 0;
	display: flex;
	width: 45%;
}
.cellIcon img {
	width: 75px;
	border: 2px solid black;
}
.lifeBarContainer {
	display: flex;
	align-items: center;
	justify-content: flex-end;
	width: 100%;
	height: 50px;
	border: 2px solid black;
	position: relative;
}
.lifeBarContainer p {
	position: absolute;
	margin-right: 0.5rem;
	color: white;
	font-weight: bold;
}
.lifeBar {
	background-color: green;
	width: 100%;
	height: 100%;
	transition: all 0.2s ease;
}
.kiContainer {
	position: absolute;
	top: 51px;
	right: 75px;
	width: 30%;
}
.kiBarContainer {
	display: flex;
	align-items: center;
	width: 100%;
	height: 25px;
	border: 2px solid black;
	position: relative;
}
.kiBarContainer .ki {
	position: absolute;
	top: 0px;
	right: 10px;
	color: white;
	font-weight: bold;
	text-shadow: 0px 0px 2px black;
}
.kiBar {
	background-color: lightseagreen;
	width: 100%;
	height: 100%;
	transition: all 0.2s ease;
}

.cell {
	position: absolute;
	bottom: 35%;
	left: 50%;
}
.cellStand {
	background: url("./../../assets/img/cell/stand/standSprites.webp") no-repeat;
	width: 215px;
	height: 350px;
	background-position: 0px 0;
	animation: cellStand 0.5s steps(4) alternate-reverse infinite;
}
.cellAttack {
	background: url("./../../assets/img/cell/attack/attackSprites.webp")
		no-repeat;
	width: 370px;
	height: 350px;
	background-position: 0px 0;
	animation: cellAttack 0.4s steps(6) alternate-reverse;
	left: 40%;
}
.cellSpecial {
	background: url("./../../assets/img/cell/special/specialAttack.webp")
		no-repeat;
	width: 319px;
	height: 350px;
	background-position: 0px 0;
	animation: cellSpecial 0.65s steps(6);
	transform: translateX(50px);
	left: 40%;
}
.cellCharge {
	background: url("./../../assets/img/cell/charge/chargeSprites.webp")
		no-repeat;
	width: 270px;
	height: 350px;
	background-position: 0px 0;
	animation: cellCharge 0.55s steps(5) alternate-reverse;
	transform: translateX(30px);
	left: 45.5%;
}
.cellEnd {
	background: url("./../../assets/img/cell/end/endSprites.webp") no-repeat;
	width: 380px;
	height: 350px;
	background-position: 0px 0;
	animation: cellEnd 1.25s steps(6);
	transform: translateX(60px);
}

@keyframes cellStand {
	to {
		background-position: -865px;
	}
}
@keyframes cellAttack {
	to {
		background-position: -2223px;
	}
}
@keyframes cellSpecial {
	to {
		background-position: -2211px;
	}
}
@keyframes cellCharge {
	to {
		background-position: -1339px;
	}
}
@keyframes cellEnd {
	to {
		background-position: -2296px;
		transform: translateX(80px);
	}
}

/* Media Query Mobile */
@media only screen and (min-width: 0px) and (max-width: 480px) {
	.cell {
		transform: scale(0.75);
		bottom: 25%;
		left: 40%;
	}
    .cellAttack {
        left: 10%;
    }
	.cellSpecial {
		left: 15%;
	}
	.cellCharge {
		left: 30%;
	}
	.cellEnd {
		left: 0%;
	}
	.cellIcon img {
		width: 35%;
	}
	.lifeBarContainer {
		height: 30px;
	}
	.kiContainer {
		top: 35px;
		right: 15.5%;
		width: 25%;
	}
	.kiBarContainer {
		height: 20px;
	}
	.kiBarContainer p {
		font-size: 0.85rem;
	}
}
</style>
