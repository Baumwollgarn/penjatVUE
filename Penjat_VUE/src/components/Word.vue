<template>
  <div class="word">
    <span v-for="letter in word" > <span v-if="isGuessed(letter)"> {{ letter }}</span> <span v-else=""> _ </span> </span>
  </div>
  <div>
      <span class="text-wrong-letters">Wrong letters: </span> <span v-for="letterWrong in wrongLetters">{{letterWrong}} </span>
  </div>
  <div>
    <span class="text-wrong-letters">Attempts left: {{attemptsLeft}}</span>
  </div>
</template>

<script>
export default {
  name: "Word",
  props: {
    word: {
      type: Array,
      required: true
    },
    guessedLetters: {
      type: Array,
      required: true
    },
    wrongLetters: {
      type: Array,
      required: false
    },
    attemptsLeft: {
      type: Number,
      required: false
    }
  },
  methods: {
    // Function to check if the letter is guessed. If so, show it, else, show an empty space
    isGuessed(letter) {
      letter = letter.toUpperCase()
      let guessedLetters = this.guessedLetters.map(letter => letter.toUpperCase())
      this.$emit('guessLetter', letter)
      return guessedLetters.includes(letter);
    }
  }
}
</script>

<style scoped>
.word {
  font-size: 3rem;
  text-align: center;
  margin: 50px;
  padding: 0;
  height: 100px;
}

.text-wrong-letters {
  font-size: 1.5rem;
  margin: 50px;
}


</style>