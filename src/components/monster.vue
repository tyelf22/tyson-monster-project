<template>
    <v-container>
    <div class="row">
        <div class="small-6 columns">
            <h1 class="text-center">YOU</h1>
            <div class="healthbar">
                <div
                        class="healthbar text-center slider"
                        :style="[ playerHealth >= 50 ? {'width': playerHealth + '%', 'background-color': 'green'} : playerHealth < 50 && playerHealth >= 15 ? {'width': playerHealth + '%', 'background-color': 'yellow', 'color': 'black'} : {'width': playerHealth + '%', 'background-color': 'red'}]">
                        
                    {{ playerHealth }}
                </div>
            </div>
        </div>
        <div class="small-6 columns">
            <h1 class="text-center">OPPONENT</h1>
            <div class="healthbar">
                <div
                        class="healthbar text-center slider"
                        :style="[ monsterHealth >= 50 ? {'width': monsterHealth + '%', 'background-color': 'green'} : monsterHealth < 50 && monsterHealth >= 15 ? {'width': monsterHealth + '%', 'background-color': 'yellow', 'color': 'black'} : {'width': monsterHealth + '%', 'background-color': 'red'}]">
                    {{ monsterHealth }}
                </div>
            </div>
        </div>
    </div>
    <div class="row controls" v-if="!gameIsRunning">
        <div class="small-12 columns">
            <v-btn rounded color="success" id="start-game" @click="startGame">START NEW GAME</v-btn>
        </div>
    </div>
    <div class="row controls" v-else>
        <div class="small-12 columns">
            <v-btn large rounded color="success" id="attack" @click="attack">SHOOT</v-btn>
            <v-btn large rounded color="error" id="special-attack" @click="specialAttack">BLOCK</v-btn>
            <v-btn large rounded color="primary" id="heal" @click="heal">3-POINTER</v-btn>
            <v-btn large rounded color="#FBFA00" id="give-up" @click="giveUp">FORFEIT</v-btn>
        </div>
    </div>
    <div class="row log" v-if="turns.length > 0">
        <div class="small-12 columns">
            <ul>
                <li v-for="turn in turns"
                    :class="{'player-turn': turn.isPlayer, 'monster-turn': !turn.isPlayer}" :key="turn.id">
                    {{ turn.text }}
                </li>
            </ul>
        </div>
    </div>
    </v-container>
</template>

<script>

import {VBtn} from 'vuetify/lib'



export default {
    data: function () {
      return {
        playerHealth: 100,
        monsterHealth: 100,
        gameIsRunning: false,
        turns: []
        }
    },
    components: function () {
        return {
        Vbtn
        }
    },
    methods: {
        startGame: function () {
            this.gameIsRunning = true;
            this.playerHealth = 0;
            this.monsterHealth = 0;
            this.turns = [];
        },

        attack: function () {
            var damage = this.calculateDamage(0, 3);
            this.monsterHealth += damage;
            this.turns.unshift({
                isPlayer: true,
                text: 'Opponent Scored ' + damage
            });
            if (this.checkWin()) {
                return;
            }

            this.monsterAttacks();
        },
        specialAttack: function () {
            var damage = this.calculateDamage(0, 3);
            this.monsterHealth -= damage;
            this.turns.unshift({
                isPlayer: true,
                text: 'Nice Defense! Opponent lost ' + damage
            });
            if (this.checkWin()) {
                return;
            }
            
        },
        heal: function () {
            if (this.playerHealth <= 100) {
                this.playerHealth += 3;
            } else {
                this.playerHealth = 100;
            }
            this.turns.unshift({
                isPlayer: true,
                text: 'Nice 3-Pointer!'
            });
            if (this.checkWin()) {
                return;
            }
            
        },
        giveUp: function () {
            this.gameIsRunning = false;
        },
        monsterAttacks: function() {
            var damage = this.calculateDamage(0, 3);
            this.playerHealth += damage;
            this.checkWin();
            this.turns.unshift({
                isPlayer: false,
                text: 'You scored ' + damage
            });
        },
        calculateDamage: function(min, max) {
            return Math.max(Math.floor(Math.random() * max) + 1, min);
        },
        checkWin: function() {
            if (this.monsterHealth >= 100) {
                if (confirm('Don\'t Be A Sore Loser!')) {
                    this.startGame();
                } else {
                    this.gameIsRunning = false;
                }
                return true;
            } else if (this.playerHealth >= 100) {
                if (confirm('Good Game! You Won!')) {
                    this.startGame();
                } else {
                    this.gameIsRunning = false;
                }
                return true;
            }
            return false;
        }
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.text-center {
    text-align: center;
}

.healthbar {
    width: 80%;
    height: 40px;
    background-color: #eee;
    margin: auto;
    transition: width 500ms;

}

.slider {
    margin: 0; 
    color: white;
}

.controls, .log {
    margin-top: 30px;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    box-shadow: 0px 3px 6px #ccc;
}

.turn {
    margin-top: 20px;
    margin-bottom: 20px;
    font-weight: bold;
    font-size: 22px;
}

.log ul {
    list-style: none;
    font-weight: bold;
    text-transform: uppercase;
}

.log ul li {
    margin: 5px;
}

.log ul .player-turn {
    color: blue;
    background-color: #e4e8ff;
}

.log ul .monster-turn {
    color: red;
    background-color: #ffc0c1;
}

button {
    font-size: 20px;
    background-color: #eee;
    padding: 12px;
    box-shadow: 0 1px 1px black;
    margin: 10px;
}

#start-game {
    background-color: #aaffb0;
}

#start-game:hover {
    background-color: #76ff7e;
}

#attack {
    background-color: #ff7367;
}

#attack:hover {
    background-color: #ff3f43;
}

#special-attack {
    background-color: #ffaf4f;
}

#special-attack:hover {
    background-color: #ff9a2b;
}

#heal {
    background-color: #aaffb0;
}

#heal:hover {
    background-color: #76ff7e;
}

#give-up {
    background-color: #ffffff;
}

#give-up:hover {
    background-color: #c7c7c7;
}
</style>
