<script lang="ts">
import { ref } from "vue";
function getRandomValue(min, max) {
  return Math.floor(Math.random() * (max - min) + min);
}

export default {
  data() {
    let monsterHealth = 100;
    let playerHealth = 100;
    let currentAtck = 0;
    let winner = null;
    let logs = [];
    let name = "Game";
    return {
      monsterHealth,
      playerHealth,
      currentAtck,
      winner,
      logs,
      name,
    };
  },
  methods: {
    log(who, what, val) {
      this.logs.unshift({
        actionBy: who,
        actionTypw: what,
        actionValue: val,
      });      
    },
    startNewGame() {
      this.monsterHealth = 100;
      this.playerHealth = 100;
      this.currentAtck = 0;
      this.winner = null;
    },
    surrender() {
      this.winner = "monster";
    },
    attackMonster() {
      this.currentAtck++;
      var attckval = getRandomValue(5, 12);
      this.monsterHealth -= attckval;
      this.logs("player", "attack", attckval);
      this.attackPlayer();
    },
    attackPlayer() {
      var attckval = getRandomValue(8, 15);
      this.playerHealth -= attckval;
      this.logs("monster", "attack", attckval);
    },
    spitialAttack() {
      this.currentAtck++;
      //   var attckval = getRandomValue(10, 17);
      //   this.monsterHealth -= attckval;
      this.monsterHealth -= 20;
      this.logs("player", "spitial-attack", 20);
      this.attackPlayer();
    },
    healPlayer() {
      var healval = getRandomValue(10, 20);
      if (this.playerHealth + healval > 100) {
        this.playerHealth = 100;
      } else {
        this.playerHealth += healval;
      }
      this.logs("player", "heal", healval);
      this.attackPlayer();
    },
  },
  computed: {
    mayUseSpetialAtck() {
      return this.currentAtck % 3 != 0;
    },
    mayUseHeal() {
      console.log(this.playerHealth);
      let res = this.playerHealth >= 100;
      return res;
    },
  },
  watch: {
    playerHealth(value) {
      if (value <= 0 && this.monsterHealth <= 0) {
        this.winner = "draw";
      } else if (value <= 0) {
        this.winner = "monster";
      }
    },
    monsterHealth(value) {
      if (value <= 0 && this.playerHealth <= 0) {
        this.winner = "draw";
      } else if (value <= 0) {
        this.winner = "player";
      }
    },
  },
};
</script>

<template>
  <v-container>
    <v-layout justify-center>
      <div id="game">
        <v-progress-linear
          class="ma-2"
          :color="monsterHealth > 50 ? 'primary' : 'error'"
          :model-value="monsterHealth < 0 ? 0 : monsterHealth"
          :height="30"
        >
          Monster Health {{ monsterHealth }}
        </v-progress-linear>
        <v-progress-linear
          class="ma-2"
          :color="playerHealth > 50 ? 'primary' : 'error'"
          :model-value="playerHealth < 0 ? 0 : playerHealth"
          :height="30"
          >Your Health {{ playerHealth }}</v-progress-linear
        >
        <v-card title="Game Over !!!" v-if="winner">
          <v-card-text v-if="winner == 'player'">You Win !</v-card-text>
          <v-card-text v-else-if="winner == 'monster'"
            >Monster Win !</v-card-text
          >
          <v-card-text v-if="winner == 'draw'">A draw !</v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
          </v-card-actions>
        </v-card>

        <section id="controls">
          <v-btn class="ma-2" @click="attackMonster">ATTACK</v-btn>
          <v-btn
            class="ma-2"
            :disabled="mayUseSpetialAtck"
            @click="spitialAttack"
            >SPECIAL ATTACK</v-btn
          >
          <v-btn
            @click="healPlayer"
            :color="playerHealth < 50 ? 'red' : ''"
            :disabled="mayUseHeal"
            class="ma-2"
            >HEAL</v-btn
          >
          <v-btn @click="surrender" class="ma-2">SURRENDER</v-btn>
          <v-btn @click="startNewGame" class="ma-2">Start New Game</v-btn>
        </section>
        <section id="log" class="container">
          <h2>Battle Log</h2>
          <ul>
            <v-list
              v-for="(log, index) in logs"
              :key="index"
            >
              {{ index }} - {{ log.actionBy }} 
            </v-list>
          </ul>
        </section>
      </div>
    </v-layout>
  </v-container>
</template>

<style scoped></style>
