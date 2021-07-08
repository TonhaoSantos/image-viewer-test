<template>
  <div>
    <h3>Pagina normal</h3>

    <button @click="changeImage('40')">40</button>
    <button @click="changeImage('15')">15</button>
    <button @click="changeImage('9')">9</button>
    <button @click="changeImage('400')">400</button>
    <button @click="changeImage('70')">70</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentImage: "40",
    };
  },
  methods: {
    changeImage(value) {
      this.$emit("change-image", value);
    },
  },
};
</script>