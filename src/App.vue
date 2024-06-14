<template>
  <h2>CSS3 Perspective Playground</h2>
  <main>
    <section class="settings">
      <div class="settings-container">
        <label>perspective: {{ perspective }}px;</label>
        <input type="range" min="0" max="999" v-model="perspective" />

        <label>rotateX: {{ rotateX }}deg; </label>
        <input type="range" min="-180" max="180" v-model="rotateX" />

        <label>rotateY: {{ rotateY }}deg; </label>
        <input type="range" min="-180" max="180" v-model="rotateY" />

        <label>rotateZ: {{ rotateZ }}deg; </label>
        <input type="range" min="-180" max="180" v-model="rotateZ" />

        <button type="button" @click.prevent="reset">Reset</button>
        <button type="button" @click.prevent="copy">Copy</button>
      </div>
    </section>
    <section class="output">
      <div class="box-container">
        <div class="box" :style="box"></div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      perspective: 100,
      rotateX: 0,
      rotateY: 0,
      rotateZ: 0,
    };
  },
  computed: {
    box() {
      return {
        transform: `
          perspective(${this.perspective}px)
          rotateX(${this.rotateX}deg)
          rotateY(${this.rotateY}deg)
          rotateZ(${this.rotateZ}deg)
        `,
      };
    },
  },
  methods: {
    reset() {
      this.perspective = 100;
      this.rotateX = 0;
      this.rotateY = 0;
      this.rotateZ = 0;
    },
    async copy() {
      let text = `transform:${this.box.transform};`;
      await navigator.clipboard.writeText(text);

      alert("CSS Copied to Clipboard!");
    },
  },
};
</script>
