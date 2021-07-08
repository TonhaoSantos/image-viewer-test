<template>
  <div class="close">
    <button @click="closeViewer">close</button>
  </div>
</template>

<script>
export default {
  name: "BaseImageViewerCloseButton",
  methods: {
    closeViewer() {
      this.$emit("close-viewer");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.close {
  position: absolute;
  top: 12px;
  right: 20px;
  z-index: 90002;
}
</style>
