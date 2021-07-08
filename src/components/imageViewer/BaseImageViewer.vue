<template>
  <div v-if="images"></div>
</template>

<script>
export default {
  name: "BaseImageViewer",
  props: {
    images: {
      type: Array,
      required: true,
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
