<template>
  <div class="buttons-zoom">
    <button @click="changeZoomTo('plus')" :disabled="disableZoomPlusButton">
      +
    </button>
    <button @click="changeZoomTo('less')" :disabled="disableZoomLessButton">
      -
    </button>
  </div>
</template>

<script>
export default {
  name: "BaseImageViewerZoomButton",
  data() {
    return {
      zoom: {
        number: 0,
        type: "",
      },
      disableZoomPlusButton: false,
      disableZoomLessButton: false,
    };
  },
  methods: {
    changeZoomTo(type) {
      let currentZoom = this.zoom.number;

      console.log(currentZoom, type);

      if (type === "plus" && currentZoom < 9) {
        currentZoom += 1;
      } else if (type === "less" && currentZoom > 0) {
        currentZoom -= 1;
      }
      console.log(currentZoom);
      if (currentZoom > 0 && currentZoom < 9) {
        this.disableZoomPlusButton = false;
        this.disableZoomLessButton = false;
      } else if (currentZoom === 9) {
        this.disableZoomPlusButton = true;
      } else if (currentZoom >= 0) {
        this.disableZoomLessButton = true;
      }

      this.zoom = {
        number: currentZoom,
        type,
      };
    },
  },
  watch: {
    zoom: {
      deep: true,
      immediate: true,
      handler(newValue, oldValue) {
        if (oldValue && newValue.number !== oldValue.number) {
          this.$emit("change-zoom", newValue);
        }
      },
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.buttons-zoom {
  position: absolute;
  top: 40px;
  left: 80px;
  z-index: 90002;
  width: 39px;
  background: red;
  height: 33px;
  overflow: hidden;
}
</style>
