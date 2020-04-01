<template>
  <main class="main">
    
    <div class="game-container">
      
      <memory-game 
        ref="game" 
        :endGame="endGame"
        @change="change"
      />
      
      <transition name="loader">
        <div v-if="endGame" class="cover">
          <button @click="reset">{{buttonStr}}</button>
        </div>
      </transition>

    </div>

    <div class="bottom-panel">
      <div class="best-panel">
        <app-text-box caption="Best" :value="bestTime" />
      </div>
      <div class="time-panel">
        <app-text-box caption="Time" :value="timerCount" align="right" />
      </div>
    </div>

  </main>
</template>

<script>
import MemoryGame from '../components/MemoryGame.vue'
import AppTextBox from '../components/AppTextBox.vue'

export default {
  name: "Index",
  components: {
    MemoryGame,
    AppTextBox,
  },

  data() {
    return {
      endGame: true,
      buttonStr: "Click to Play",
      bestTime: 0,
      timer: null,
      timerCount: 0,
    }
  },

  head() {
    return {
      title: "vue-memory-game",
    }
  },

  methods: {
    
    startTimer: function() {
      this.timer = setInterval(() => {
        this.timerCount++;
      }, 1000)
    },

    stopTimer: function() {
      clearInterval(this.timer)

      if(this.bestTime === 0) {
        this.bestTime = this.timerCount;
      } else {
        if(this.bestTime > this.timerCount) {
          this.bestTime = this.timerCount;
        }
      }
    },

    change: function(status) {
      
      if(status === "finish") {
        
        this.stopTimer()
        
        setTimeout(()=>{
          
          this.buttonStr = "Try Again?";
          this.endGame = true;
        
        },1000)        
      
      } else if(status === "start") {
        
        if(!this.endGame) {
          this.timerCount = 0;
          this.startTimer()
        }

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
  background-color: white;
  position: relative;
  width: 220px;
  margin: 0px auto;
  z-index: 1;
  overflow: hidden;
}

.bottom-panel {
  position: relative;
  width: 220px;
  margin: 2px auto;
}
.best-panel, .time-panel {
  width: 110px;
  float: left;
}

.cover {
  background-color: transparent;
  position: absolute;
  left: 0px;
  top: 0px;
  width: 220px;
  height: 308px;
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

.loader-enter-active {
  animation: loader-in .5s;
}
.loader-leave-active {
  animation: loader-in .5s reverse;
}
@keyframes loader-in {
  0% {
    transform: scale(0, 0) rotate(720deg);
    opacity: 0;
  }
  50% {
    transform: scale(2, 2) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: scale(1, 1);
    opacity: 1;
  }
}
</style>