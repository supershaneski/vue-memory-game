<template>
    <div class="card-container" @click="click">
        <div class="card" :class="{ flipped: flipped }">
            <transition name="rotate-hide">
                <div v-if="show" class="cell">
                    
                    <img v-if="src === 'apple.jpg'" class="front" src="/apple.jpg" />
                    <img v-if="src === 'banana.jpg'" class="front" src="/banana.jpg" />
                    <img v-if="src === 'coconut.jpg'" class="front" src="/coconut.jpg" />
                    <img v-if="src === 'grapes.jpg'" class="front" src="/grapes.jpg" />

                    <img v-if="src === 'guava.jpg'" class="front" src="/guava.jpg" />
                    <img v-if="src === 'melon.jpg'" class="front" src="/melon.jpg" />
                    <img v-if="src === 'orange.jpg'" class="front" src="/orange.jpg" />
                    <img v-if="src === 'pears.jpg'" class="front" src="/pears.jpg" />
                    
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
            default: 'apple.jpg',
        },
    },

    data() {
        return {
            flipped: false,
            show: true,
            frontImage: "/trump.jpg",
        }
    },

    methods: {

        click: function() {
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
    transition: 1s;
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
  transition: all .5s;
}

.rotate-hide-enter, .rotate-hide-leave-to {
  transform: scale(0, 0) rotate(360deg);
}
</style>