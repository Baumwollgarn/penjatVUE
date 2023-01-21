<template>
  <!-- conditional class if the letter is guessed and correct, add the class correct -->
  <div class="letter-single" @click="guessLetter" :class="{correct: isGuessed && isCorrect, wrong: isGuessed && !isCorrect}">
    {{letter}}
  </div>
</template>

<script>
export default {
  name: "Letter",
  props: {
    letter: {
      type: String,
      default: () => 'a'
    },
    isGuessed: {
      type: Boolean,
      default: () => false
    },
    isCorrect: {
      type: Boolean,
      default: () => false
    }
  },
  methods: {
    guessLetter() {
      this.$emit('guessLetter', this.letter)
    }
  }
}
</script>

<style scoped>

.letter-single {
  background: mintcream;
  width: 40px;
  text-align: center;
  border: #2c3e50 1px solid;
  border-radius: 50%;
  color: #2c3e50;
}

.letter-single:hover {
  background: #e1e1e1;
  cursor: pointer;
}

.wrong {
  background: #e74c3c;
  color: white;
}

.correct {
  background: #2ecc71;
  color: white;
}

</style>