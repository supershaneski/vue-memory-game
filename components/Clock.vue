<template>
    <span>{{timeStr}}</span>
</template>

<script>
export default {
    name: "Clock",
    data() {
        return {
            timer: null,
            timeStr: (new Date()).toLocaleTimeString(),
        }
    },
    mounted() {
        this.timer = setInterval(() => {
            this.timeStr = (new Date()).toLocaleTimeString();
        }, 1000)
    },
    beforeDestroy() {
        clearInterval(this.timer)
    }
}
</script>

<style scoped>
span {
    color: #ccc;
}
</style>