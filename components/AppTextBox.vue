<template>
    <div class="app-textbox-container" :style="cssProps">
        <span class="app-textbox-caption">{{ caption }}:</span>
        <span class="app-textbox-text">{{ displayText }}</span>
    </div>
</template>

<script>
export default {
    name: 'AppTextBox',
    props: {
        caption: String,
        value: {
            type: Number,
            default: 0,
        },
        color: {
            type: String,
            default: '#000',
        },
        align: {
            type: String,
            default: 'left',
        }
    },
    computed: {
        cssProps() {
            return {
                '--text-color': this.color,
                '--text-align': this.align,
            }
        },
        displayText() {
            let str = "0000";
            const num = this.value;
            if(num < 10) {
                str = "000" + num;
            } else if(num >= 10 && num < 100) {
                str = "00" + num;
            } else if(num >= 1000 && num < 10000) {
                str = "0" + num;
            } else {
                str = num;
            }
            return str;
        }
    }
}
</script>

<style scoped>
.app-textbox-container {
    background-color: transparent;
    position: relative;
    text-align: var(--text-align);
    color: var(--text-color);
}
span {
    font-family: "Comic Sans MS", Avenir, Helvetica, Arial, sans-serif;
    font-size: 0.9em;
}
.app-textbox-caption {
    font-weight: 600;
    text-transform: uppercase;
    padding-right: 5px;
}
</style>