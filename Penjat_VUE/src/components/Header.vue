<template>
  <div>
    <h1>Hangman</h1>
    <p>Find the hidden word - Enter a letter</p>
  </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style scoped>
h1 {
  text-align: center;
  font-size: 4rem;
  margin: 0;
  padding: 0;
}

p {
  text-align: center;
  font-size: 1.5rem;
  margin: 0;
  padding: 0;
}

div {
  background-color: transparent;
  width: 550px;
  margin: 0 auto;
  color: black;
  padding: 1rem;
}

</style>