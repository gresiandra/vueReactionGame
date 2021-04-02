<template>
    <div v-if="showingBlock" class="block" :style="[wideScreen ? none : stylePhone]">
        <button class="clickMe" @click="stopGame" :style="[wideScreen ? styleWide : none]">Click Me</button>
    </div>
</template>

<script>
export default {
    name: 'Block',
    props: ['delay'],
    data() {
        return {
            showingBlock: false,
            startTime: 0,
            endTime: 0,
            score: 0,
            wideScreen: false,
            styleWide: {
                position: 'absolute',
                top: `${Math.round(Math.random() * 315)}px`,
                left: `${Math.round(Math.random() * 695)}px`,
            },
            stylePhone: {
                width: '350px',
                height: '200px',
                justifyContent: 'center',
                alignItems: 'center',
                backgroundColor: 'white',
                border: 'none'
            }
        }
    },
    created(){
        if (window.screen.width >= 800) {
            this.wideScreen = true
        } else {
            this.wideScreen = false
        }
    },
    methods: {
        stopGame(){
            this.endTime = new Date().getTime()
            console.log(`end time: ${this.endTime}`)

            this.score = this.endTime - this.startTime
            this.showingBlock = false

            this.$emit('end', this.score)
        }
    },
    mounted(){
        setTimeout(() => {
            this.showingBlock = !this.showingBlock
            this.startTime = new Date().getTime()
            console.log(`start time: ${this.startTime}`)
        }, this.delay);
    },
}
</script>

<style>
    .block {
        width: 800px;
        height: 400px;
        background-color: rgba(144, 238, 144, 1);
        position: relative;
        border-radius: 10px;
        border: 2px solid black;
        display: flex;
    }

    .block .clickMe {
        width: 100px;
        height: 50px;
        border: 2px solid black;
        background: white;
        cursor: pointer;
    }
</style>