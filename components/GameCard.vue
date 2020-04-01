<template>
    <div class="card-container" @click="click">
        <div class="card" :class="{ flipped: flipped }">
            <transition name="rotate-hide">
                <div v-if="show" class="cell">
                    
                    <img v-if="src === 'brook.jpg'" class="front" src="/brook.jpg" />
                    <img v-if="src === 'chopper.jpg'" class="front" src="/chopper.jpg" />
                    <img v-if="src === 'luffy.jpg'" class="front" src="/luffy.jpg" />
                    <img v-if="src === 'nami.jpg'" class="front" src="/nami.jpg" />

                    <img v-if="src === 'robin.jpg'" class="front" src="/robin.jpg" />
                    <img v-if="src === 'sanji.jpg'" class="front" src="/sanji.jpg" />
                    <img v-if="src === 'ussop.jpg'" class="front" src="/ussop.jpg" />
                    <img v-if="src === 'zoro.jpg'" class="front" src="/zoro.jpg" />
                    
                    <img class="back" src="/back.jpg" />
                </div>
            </transition>
        </div>
    </div>
</template>

<script>
export default {
    name: "GameCard",
    props: {
        src: {
            type: String,
            default: 'luffy.jpg',
        },
    },

    data() {
        return {
            flipped: false,
            show: true,
        }
    },

    methods: {

        click: function() {
            if(!this.show) return;
            this.$emit('click', this.src)
        },

        flip: function(flag){
            this.flipped = flag
        },

        showHide: function(flag) {
            this.show = flag;
            if(this.show) {
                this.flipped = false;
            }
        },
    },
}
</script>

<style scoped>

.card-container {
    background-color: transparent;
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 53px;
    height: 75px;
    border: 1px solid transparent;
    cursor: pointer;
}

.card {
    position: relative;
    width: 75px;
    height: 75px;
    transform: scale(1.0, 1.0) rotate(0deg);
    transition: .5s;
    transform-style: preserve-3d;
}

.card img {
    position: absolute;
    left: 0px;
    top: 0px;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
}

.cell {
    position: absolute;
    left: 0px;
    top: 0px;
    width: 100%;
    height: 100%;
}

.front {
    z-index: 2;
    transform: rotateY(180deg);
}

.back {
    z-index: 1;
    transform: rotateY(0deg);
}

.flipped {
    transform: rotateY(180deg);
}

.rotate-hide-enter-active, .rotate-hide-leave-active {
  transition: all .3s;
}

.rotate-hide-enter, .rotate-hide-leave-to {
  transform: scale(0, 0) rotate(360deg);
}
</style>