<template>
  <div class="letters">
   <slot></slot>
  </div>
</template>

<script>

import Letter from "@/components/Letter.vue";

export default {
  name: "Letters",
  props: {
  },
  components: {
    Letter
  },
  data() {
    return {
      letters: []
    }
  }
}
</script>

<style scoped>

span {
  display: inline-block;
  width: 30px;
  height: 30px;
  border: 1px solid black;
  margin: 5px;
  text-align: center;
  line-height: 30px;
  font-size: 1.5rem;
  color: white;
}

.letters {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 0 auto;
  width: 750px;
  gap: 10px;
  font-size: 22px;
}
</style>