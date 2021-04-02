<template>
    <div class="start-container">
      <h1>Reaction Test!</h1>
      <button :disabled="buttons"  @click="playGame"> {{ buttonText }} </button>
      <Block v-if="showBlock" :delay="delay" @end="endGame"/>

      <div class="result" v-show="showResult">
        <h2>Reaction time: <span> {{ finalScore }} sec </span></h2>
      </div>
    </div>

</template>

<script>
import Block from './components/Block'

export default {
    name: 'App',
    components: { Block },
    data() {
      return {
        showBlock: false,
        buttons: false,
        delay: null,
        showResult: false,
        finalScore: 0,
        buttonText: 'Start'
      }
    },
    methods: {
      playGame() {
        this.buttons = true
        this.showBlock = true
        this.showResult = false
        this.delay = 1000 + Math.random() * 14000
        this.buttonText = 'Wait'
      },
      endGame(score) {
        console.log(`final score ${score} ms`)
        this.buttons = false
        this.showBlock = false
        this.finalScore = Math.round(score) *0.001
        this.finalScore = this.finalScore.toFixed(3)
        this.showResult = true
        this.buttonText = 'Start'
      }
    }
}
</script>

<style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Chakra Petch', sans-serif;
    }

    body {
      max-width: 800px;
      margin: 50px auto;
    }

    .start-container {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }

    button {
      border-radius: 10px;
      width: 100px;
      height: 50px;
      margin-top: 30px;
      margin-bottom: 30px;
      background: rgba(144,238,144,1);
      border: 2px solid black;
      cursor: pointer;
      font-weight: 600;
      letter-spacing: 0.1rem;
    }

    .result {
      margin-top: 30px;
      font-weight: 300;
    }

    .result span {
      width: 100%;
      color: rgb(219, 57, 57);
      font-size: 2.5rem;
      font-weight: 600;
    }

    @media screen and (max-width: 500px) {
      .result {
        width: 300px;
        text-align: center;
      }

      .result span {
        display: block;
        text-align: center;
        width: 300px;
      }
    }
</style>
