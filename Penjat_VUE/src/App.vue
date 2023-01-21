<template>
  <!-- Hangman image -->

  <div class="game-container">
    <Word :word="word" :guessedLetters="guessedLetters" :wrongLetters="wrongLetters" :attempts-left="attemptsLeft"/>
    <Letters>
      <Letter v-for="letter in letters" :letter="letter" @guess-letter="guessLetter" :isGuessed="isGuessed(letter)" :isCorrect="isCorrect(letter)"></Letter>
    </Letters>
    <div class="message-container" @keyup.enter="resetGame">
      {{message}}
    </div>
  </div>

</template>

<script>

import Header from './components/Header.vue'
import Letters from "@/components/Letters.vue";
import Letter from "@/components/Letter.vue";
import Word from "@/components/Word.vue";

const words = ['programming', 'vuejs', 'composition', 'linux', 'windows', 'macos', 'javascript', 'typescript', 'reactjs', 'angularjs', 'google', 'requirement', 'interaction', 'engineering']
let randomWord = words[Math.floor(Math.random() * words.length)]
randomWord = randomWord.toUpperCase().split('')

let letters = 'abcdefghijklmnopqrstuvwxyz'.split('')
letters = letters.map(letter => letter.toUpperCase())
export default {
  components: {Word, Letter, Letters, Header},
  data() {
    return {
      letters,
      word: randomWord,
      guessedLetters: [],
      wrongLetters: [],
      message: '',
      attemptsLeft: 7,
      isFinished: false
    }
  },
  methods: {
    checkWin() {
      if (this.word.every(letter => this.guessedLetters.includes(letter))) {
        this.message = 'You win! Press any key to play again'
        this.isFinished = true
        this.letters = []
      }
      if (this.wrongLetters.length === 7) {
        this.message = `You lose! The word was ${this.word.join('')}. Press any key to play again`
        this.isFinished = true
        this.letters = []
      }
    },
    guessLetter(letter) {
      letter = letter.toUpperCase()
      if (!this.guessedLetters.includes(letter)) {
        this.guessedLetters.push(letter)
        if (!this.word.includes(letter)) {
          this.message = `${letter} is not in the word`
          this.wrongLetters.push(letter)
        }
      }
      this.calculateAttemptsLeft()
      this.checkWin()
    },
    isGuessed(letter) {
      letter = letter.toUpperCase()
      let guessedLetters = this.guessedLetters.map(letter => letter.toUpperCase())
      return guessedLetters.includes(letter);
    },
    isCorrect(letter) {
      letter = letter.toUpperCase()
      return this.word.includes(letter)
    },
    calculateAttemptsLeft() {
      this.attemptsLeft = 7 - this.wrongLetters.length
    },
    resetGame() {
      this.guessedLetters = []
      this.wrongLetters = []
      this.message = ''
      this.attemptsLeft = 7
      randomWord = words[Math.floor(Math.random() * words.length)]
      randomWord = randomWord.toUpperCase().split('')
      this.word = randomWord
      this.letters = 'abcdefghijklmnopqrstuvwxyz'.split('')
      this.letters = this.letters.map(letter => letter.toUpperCase())
      this.isFinished = false
    },
    handleKeyup(e) {
      console.log(e.key)
      if (!this.isFinished && e.key.length < 2) {
        this.guessLetter(e.key)
      } else if (this.isFinished) {
        this.resetGame()
      }
    }
  },
  mounted() {
    window.addEventListener('keyup', this.handleKeyup)
  },
  beforeDestroy() {
    window.removeEventListener('keyup', this.handleKeyup)
  }
}
</script>

<style scoped>

.message-container {
  text-align: center;
  font-size: 2rem;
  margin: 50px;
}
</style>