<template>
  <div id="app">
    <p>Tela</p>
    <BaseImageViewerImage :images="imageList" />
  </div>
</template>

<script>
import BaseImageViewerImage from "./components/imageViewer/BaseImageViewerImage";
import { ramdomImageList } from "./enums/imagesList";

export default {
  name: "App",
  components: {
    BaseImageViewerImage,
  },
  data() {
    return {
      currentImage: "", // 15 9 400 70 40
    };
  },
  computed: {
    imageList() {
      return ramdomImageList;
    },
  },
  methods: {
    changeImage(value) {
      let currentValue = value;

      if (this.currentImage === value) currentValue = "";
      this.currentImage = currentValue;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
*,
*::before,
*::after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
