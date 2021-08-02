<template>
  <div @click="onClick" class="drum">
    <div
      v-for="(kick, index) in kicks"
      :key="index"
      :class="transport === index ? 'transportOn' : ''"
    >
      X
    </div>
    <div
      v-for="(kick, index) in kicks"
      :key="index"
      data-type="kicks"
      :data-idx="index"
    >
      {{ kick }}
    </div>
    <div
      v-for="(snare, index) in snares"
      :key="index"
      data-type="snares"
      :data-idx="index"
    >
      {{ snare }}
    </div>
    <div
      v-for="(hat, index) in hats"
      :key="index"
      data-type="hats"
      :data-idx="index"
    >
      {{ hat }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Drummer",
  props: {
    kicks: Array,
    snares: Array,
    hats: Array,
    transport: Number,
  },
  methods: {
    onClick(e) {
      this.$emit("toggle", {
        key: e.target.dataset.type,
        idx: e.target.dataset.idx,
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.drum {
  width: 200px;
  background: yellow;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  cursor: pointer;
  background-size: contain;
}
.transportOn {
  background: red;
}
</style>
