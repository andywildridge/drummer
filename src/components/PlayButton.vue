<template>
  <div>
    <button @click="play()">{{ text }}</button>
    <button @click="stop()">Stop</button>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
  },
  methods: {
    play() {
      this.$emit("play");
    },
    stop() {
      this.$emit("stop");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  background: green;
  margin: 10px;
}
</style>
