<template>
  <PlayButton text="play" @play="play" @stop="stop" />
  <Drummer
    @toggle="toggle"
    :kicks="kicks"
    :snares="snares"
    :hats="hats"
    :transport="transport"
  />
</template>

<script>
import Drummer from "./components/Drummer";
import PlayButton from "./components/PlayButton";
import * as Tone from "tone";

export default {
  name: "App",
  components: {
    Drummer,
    PlayButton,
  },
  data() {
    return {
      kicks: [1, 0, 0, 0, 0, 0, 0, 0],
      snares: [0, 0, 0, 0, 1, 0, 0, 0],
      hats: [1, 1, 1, 1, 1, 1, 1, 1],
      transport: 3,
    };
  },
  created() {
    this.synth = new Tone.Synth().toDestination();
    this.synthH = new Tone.Synth().toDestination();
    this.pattern = new Tone.Pattern(
      (time, index) => {
        console.log(time, index, this.kicks[index]);
        this.transport = index;
        if (this.kicks[index]) {
          this.synth.triggerAttackRelease("E4", "32n", time);
        }
        if (this.snares[index]) {
          this.synth.triggerAttackRelease("F4", "32n", time);
        }
        if (this.hats[index]) {
          this.synthH.triggerAttackRelease("G4", "32n", time, 0.2);
        }
      },
      [0, 1, 2, 3, 4, 5, 6, 7],
      "up"
    ).start(0);
  },
  methods: {
    toggle(e) {
      console.log(e);
      this[e.key][e.idx] = 1 - this[e.key][e.idx];
    },
    play() {
      //play a middle 'C' for the duration of an 8th note
      this.synth.triggerAttackRelease("C4", "16n", 0, 0);
      Tone.Transport.start();
    },
    stop() {
      // this.synth.triggerAttackRelease("D4", "16n");
      Tone.Transport.pause();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
