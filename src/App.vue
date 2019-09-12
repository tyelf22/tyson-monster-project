<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">Monster</span>
        <span class="font-weight-heavy">Project</span>
      </v-toolbar-title>
      <v-btn
        text
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
      </v-btn>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>

<!-- <div id="app">
    <section class="row">
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
            <h1 class="text-center">MONSTER</h1>
            <div class="healthbar">
                <div
                        class="healthbar text-center slider"
                        :style="[ monsterHealth >= 50 ? {'width': monsterHealth + '%', 'background-color': 'green'} : monsterHealth < 50 && monsterHealth >= 15 ? {'width': monsterHealth + '%', 'background-color': 'yellow', 'color': 'black'} : {'width': monsterHealth + '%', 'background-color': 'red'}]">
                    {{ monsterHealth }}
                </div>
            </div>
        </div>
    </section>
    <section class="row controls" v-if="!gameIsRunning">
        <div class="small-12 columns">
            <button id="start-game" @click="startGame">START NEW GAME</button>
        </div>
    </section>
    <section class="row controls" v-else>
        <div class="small-12 columns">
            <button id="attack" @click="attack">ATTACK</button>
            <button id="special-attack" @click="specialAttack">SPECIAL ATTACK</button>
            <button id="heal" @click="heal">HEAL</button>
            <button id="give-up" @click="giveUp">GIVE UP</button>
        </div>
    </section>
    <section class="row log" v-if="turns.length > 0">
        <div class="small-12 columns">
            <ul>
                <li v-for="turn in turns"
                    :class="{'player-turn': turn.isPlayer, 'monster-turn': !turn.isPlayer}" :key="turn.id">
                    {{ turn.text }}
                </li>
            </ul>
        </div>
    </section>
</div> -->

</template>

<script>
import HelloWorld from './components/HelloWorld';
import { VApp, VAppBar, VToolbarTitle, VContent, VBtn} from 'vuetify/lib'


export default {
  name: 'App',
  components: {
    HelloWorld,
    VApp,
    VAppBar,
    VToolbarTitle,
    VContent,
    VBtn
  },
  data: () => ({
    //
  }),
};

</script>
