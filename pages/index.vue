<template>
  <main class="main">
    <clock />
    <div class="game-container">
      <memory-game 
        ref="game" 
        :endGame="endGame"
        @change="change"
      />
      <div v-if="endGame" class="cover">
        <button @click="reset">{{buttonStr}}</button>
      </div>
    </div>
  </main>
</template>

<script>
import MemoryGame from '../components/MemoryGame.vue'
import Clock from '../components/Clock.vue'

export default {
  name: "Index",
  components: {
    MemoryGame,
    Clock,
  },

  data() {
    return {
      endGame: true,
      buttonStr: "Click to Play",
    }
  },

  head() {
    return {
      title: "vue-memory-game",
    }
  },

  methods: {
    
    change: function(status) {
      if(status === "finish") {
        this.buttonStr = "Try Again?";
        this.endGame = true;
      }
    },
    
    reset: function() {
      this.$refs.game.reset()
      this.endGame = false;
    }
    
  },
}
</script>

<style scoped>

.main {
  background-color: transparent;
}

.game-container {
  background-color: #e6e6e6;
  position: relative;
  width: 220px;
  margin: 0px auto;
  padding: 10px;
  z-index: 1;
}

.cover {
  background-color: transparent;
  position: absolute;
  left: 0px;
  top: 0px;
  width: 240px;
  height: 328px;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  border: 2px solid white;
  background-color: black;
  padding: 10px 20px;
  border-radius: 8px;
  outline: none;
  color: white;
  letter-spacing: 1px;
  cursor: pointer;
}

button:hover {
  background-color: gray;
}

button:active {
  background-color: #e6e6e6;
  color: #222;
}
</style>