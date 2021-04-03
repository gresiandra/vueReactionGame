<template>
    <div class="start-container">
      <h1>Reaction Test!</h1>
      <p class="hint">Press 'Start' button and wait... <br> after awhile another button will appear and click it as fast as you could!</p>
      <button :disabled="buttons"  @click="playGame"> {{ buttonText }} </button>
      <Block v-if="showBlock" :delay="delay" @end="endGame"/>

      <div class="result" v-show="showResult">
        <h2>Reaction time: <span> {{ finalScore }} sec </span></h2>
        <p class="textresult">{{ textResult }}</p>
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
        textResult: null,
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

        if (score > 0 && score <= 300) {
          this.textResult = `Are you THE FLASH?!`
        } else if (score > 300  && score <= 500) {
          this.textResult = `Wow that's quick`
        } else if (score > 500  && score <= 1000) {
          this.textResult = `You could do Better`
        } else if (score > 1000) {
          this.textResult = `Zzzzzzzzzz. . .`
        }

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
      margin: 40px auto;
    }

    .start-container {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    
    .hint {
      margin-top: 10px;
      font-weight: 300;
      text-align: center;
      padding: 10px 20px;
    }

    button {
      border-radius: 10px;
      width: 100px;
      height: 50px;
      margin-top: 20px;
      margin-bottom: 25px;
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

    .textresult {
      font-weight: 700;
      text-align: center;
      margin-top: 10px;
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
