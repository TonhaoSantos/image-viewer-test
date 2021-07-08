<template>
  <div class="slider" :class="{ expandido: expanded }">
    <div class="slider-expandir">
      <button @click="changeExpanded">expandir</button>
      Ola mundo
    </div>

    <div class="slider-content">
      <button
        class="prev-next-button prev-button"
        @click="changeImagePrevNext('prev')"
      >
        prev
      </button>

      <ul class="slider__list">
        <li
          v-for="(item, index) in images"
          :key="index"
          class="slider__list-item"
          @click="changeImage(index)"
        >
          <img :src="item.img" alt="" class="slider__list-img" />
        </li>
      </ul>

      <button
        class="prev-next-button next-button"
        @click="changeImagePrevNext('next')"
      >
        next
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "BaseImageViewerSlider",
  props: {
    images: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      expanded: true,
    };
  },
  methods: {
    changeExpanded() {
      this.expanded = !this.expanded;
    },
    changeImage(index) {
      this.$emit("change-image", index);
    },
    changeImagePrevNext(type) {
      this.$emit("change-image-prev-next", type);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.slider {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 90002;
  height: 30px;
  overflow: hidden;
  background: red;
}
.expandido {
  height: 90px;
}
.slider-expandir {
  height: 30px;
  background: blueviolet;
  overflow: hidden;
  position: relative;
}
.slider-content {
  height: 60px;
  background: blueviolet;
  overflow: hidden;
  position: relative;
}
.slider__list {
  list-style-type: none;
  background: tomato;
  display: flex;
  justify-content: center;
}
.slider__list-item {
  position: relative;
  display: inline-block;
}
.slider__list-item:hover {
  cursor: pointer;
}
.slider__list-img {
  width: 60px;
  height: 48px;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -webkit-user-drag: none;
  user-drag: none;
  -webkit-touch-callout: none;
}
.prev-next-button {
  position: absolute;
}
.prev-next-button:hover {
  cursor: pointer;
}
.prev-next-button.prev-button {
  top: 16px;
  left: 0;
}
.prev-next-button.next-button {
  top: 16px;
  right: 0;
}
</style>
