<template>
    <div class="memory-game">
        <transition-group name="cello" tag="div" class="container">
            <game-card 
                @click="img => click(item.index, img)" 
                :src="item.image" 
                :ref="`card-${item.index}`" 
                class="cello" 
                v-for="item in cardItems" 
                :key="item.index"
            />
        </transition-group>        
    </div>
</template>

<script>
import GameCard from '../components/GameCard.vue'
import Lib from '../lib/utils'
import _ from 'lodash'

export default {
    name: "MemoryGame",
    components: {
        GameCard,
    },

    props: {
        endGame: {
            type: Boolean,
            default: true,
        },
    },

    data() {
        return {
            //items: [],
            cardItems: [],
            selected: [],
            flag: false,
            count: 0,
        }
    },

    methods: {
        click(index, image) {
            
            if(this.endGame) return;

            if(this.flag) return;
            
            if(this.selected.length === 1) {
                
                if(this.selected[0].index === index) return;

                this.$refs['card-' + index][0].flip(true)
                this.selected.push({
                    index: index,
                    image: image
                })

                this.flag = true;

                if(this.selected[0].image === image) {
                    setTimeout(() => {
                        this.count++;
                        this.flag = false;
                        this.hideSelected()
                        
                        if(this.count >= 8) {
                            this.$emit('change','finish')
                        }

                    }, 1000)
                } else {
                    setTimeout(() => {
                        this.flag = false;
                        this.resetSelected()
                    }, 1000)
                }
            } else {
                this.$refs['card-' + index][0].flip(true)
                this.selected.push({
                    index: index,
                    image: image
                })
            }
            
        },

        resetSelected: function() {
            const previndex = this.selected[0].index;
            const curindex = this.selected[1].index;
            
            this.$refs['card-' + previndex][0].flip(false)
            this.$refs['card-' + curindex][0].flip(false)

            this.selected = [];
        },

        hideSelected: function() {
            const previndex = this.selected[0].index;
            const curindex = this.selected[1].index;
            
            this.$refs['card-' + previndex][0].showHide(false)
            this.$refs['card-' + curindex][0].showHide(false)

            this.selected = [];
        },

        /*
        shuffle: function() {
            this.cardItems = _.shuffle(this.cardItems);
        },

        flipAll: function() {
            for(var i = 0; i < 16; i++) {
                this.$refs['card-'+i][0].flip(false)
            }
        },
        
        showHide: function() {
            for(var i = 0; i < 16; i++) {
                this.$refs['card-'+i][0].showHide(true)
            }
        },
        */

        reset: function() {
            this.cardItems = _.shuffle(this.cardItems);
            for(var i = 0; i < 16; i++) {
                this.$refs['card-'+i][0].showHide(true)
            }
        },
    },

    created() {
        const images = [
            "apple.jpg",
            "banana.jpg",
            "coconut.jpg",
            "grapes.jpg",
            "guava.jpg",
            "melon.jpg",
            "orange.jpg",
            "pears.jpg",
        ]
        for(var i = 0; i < 16; i++) {
            this.cardItems.push({
                id: images[i%8].replace(".jpg","") + i,
                index: i,
                image: images[i%8],
                flip: false,
                show: true,
            })
        }
    },

    mounted() {
        console.log("mounted")
    },

    updated() {
        console.log("updated")
        this.$emit('change','start')
        this.count = 0;
    }
}
</script>

<style scoped>

.memory-game {
    background-color: transparent;
    position: relative;
    width: 220px;
    height: 308px;
    display: flex;
    flex-wrap: wrap;
}

.container {
    background-color: transparent;
    display: flex;
    flex-wrap: wrap;
    width: 220px;
}

.cello-move {
    transition: transform 1s;
}
</style>