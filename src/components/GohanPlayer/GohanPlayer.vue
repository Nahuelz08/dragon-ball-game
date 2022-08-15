<template>
	<div>
        <div class="gohanIcon">
            <img src="./../../assets/img/gohan/gohan-icon.webp" :style="playerDefeated" alt="">
            <div class="lifeBarContainer">
                <p>GOHAN</p>
                <div class="lifeBar" :style="setPlayerLife"></div>
            </div>
        </div>
        <div class="kiContainer">
            <div class="kiBarContainer">
                <div class="kiBar" :style="setKiNumber"></div>
                <p class="ki">Ki: {{playerKiNumber}}%</p>
            </div>
        </div>
		<i :class="'gohan ' + playerAction"></i>
	</div>
</template>

<script>
export default {
	data() {
		return {
			
		};
	},
    props: ['player-life', 'playerKiNumber', 'player-action'],
    computed: {
        setPlayerLife() {
            if (this.playerLife <= 0) {
                return { width: '0%', backgroundColor: 'red' }
            } else {
                return { width:this.playerLife + '%'}
            }
        },
        setKiNumber() {
            if (this.playerKiNumber <= 0) {
                return { width: '0%' }
            } else {
                return { width:this.playerKiNumber + '%'}
            }
        },
        playerDefeated() {
            if (this.playerLife <= 0) {
                return { filter: 'grayscale(1)' }
            } else {
                return { filter: 'grayscale(0)'}
            }
        }
    }
};
</script>

<style scoped>
.gohanIcon {
	position: absolute;
    top: 0;
    display: flex;
    width: 45%;
}
.gohanIcon img{
    width: 75px;
    border: 2px solid black;
}
.lifeBarContainer {
    display: flex;
    align-items: center;
    width: 100%;
    height: 50px;
    border: 2px solid black;
    position: relative;
}
.lifeBarContainer p{
    position: absolute;
    margin-left: 0.5rem;
    color: white;
    font-weight: bold;
}
.lifeBar {
    background-color: green;
    width:100%;
    height: 100%;
    transition: all 0.2s ease;
}
.kiContainer {
    position: absolute;
    top: 51px;
    left: 75px;
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
.kiBarContainer .ki{
    position: absolute;
    top: 0;
    left: 10px;
    color: white;
    font-weight: bold;
    text-shadow: 0px 0px 2px black;
}
.kiBar {
    background-color: lightseagreen;
    width:100%;
    height: 100%;
    transition: all 0.2s ease;
}

.gohan {
    transform: scaleX(-1);
    position: absolute;
    bottom: 35%;
    right: 60%;
}
.gohanStand {
	background: url('./../../assets/img/gohan/stand/standSprites.webp') no-repeat;
	width: 100px;
	height: 243px;
	background-position: 0px 0;
	animation: gohanStand 0.5s steps(4) alternate-reverse infinite;
}

.gohanAttack {
	background: url('./../../assets/img/gohan/attack/attackSprites.webp') no-repeat;
	width: 220px;
	height: 243px;
	background-position: 0px 0;
	animation: gohanAttack 0.4s steps(5) alternate-reverse;
    right: 50%;
}

.gohanSpecial {
	background: url('./../../assets/img/gohan/special/specialSprites.webp') no-repeat;
	width: 165px;
	height: 243px;
	background-position: 0px 0;
	animation: gohanSpecial 0.65s steps(6) ;
    right: 55%;
}

.gohanCharge {
	background: url('./../../assets/img/gohan/charge/chargeSprites.webp') no-repeat;
	width: 150px;
	height: 243px;
	background-position: 0px 0;
	animation: gohanCharge 0.55s steps(6) alternate-reverse;
    right: 57%;
}
.gohanEnd {
	background: url('./../../assets/img/gohan/end/endSprites.webp') no-repeat;
	width: 170px;
	height: 243px;
	background-position: 0px 0;
	animation: gohanEnd 1.25s steps(7) ;
    right: 55%;
}

@keyframes gohanStand {
	to {
		background-position: -400px;
	}
}
@keyframes gohanAttack {
	to {
		background-position: -1151px;
	}
}
@keyframes gohanSpecial {
	to {
		background-position: -989px;
	}
}
@keyframes gohanCharge {
	to {
		background-position: -885px;
	}
}
@keyframes gohanEnd {
	to {
		background-position: -1170px;
	}
}

/* Media Query Mobile */
@media only screen and (min-width:0px) and (max-width: 480px){
    .gohan {
        transform: scale(-0.75, 0.75);
        bottom: 27%;
        right: 60%;
    }
    .gohanAttack {
        right: 30%;
    }
    .gohanSpecial {
        right: 45%;
    }
    .gohanCharge {
        right: 50%;
    }
    .gohanEnd {
        right: 45%;
    }
    .gohanIcon img {
        width: 35%;
    }
    .lifeBarContainer {
        height: 30px;
    }
    .kiContainer {
        top: 35px;
        left: 15.5%;
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
