<template>
  <div v-if="isValid">
    <div>
      <ul id="images" ref="images" class="base-image-viewer">
        <li
          v-for="(item, index) in images"
          :key="index"
          style="display: inline-block"
        >
          <img
            :src="item.img"
            :alt="`Picture ${index + 1}`"
            style="width: 70px"
            @click="selectImage"
          />
        </li>
      </ul>
    </div>

    <div v-if="showModal">
      <BaseImageViewerZoomButton
        @change-zoom="changeZoom"
        class="base-image-tools-itens"
      />
      <br />
      <BaseImageViewerCloseButton @close-viewer="fechar" />
      <br />
      <BaseImageViewerSlider
        :images="images"
        @change-image="changeImage"
        @change-image-prev-next="changeImagePrevNext"
      />
      <div class="base-image-tools"></div>
    </div>
  </div>
</template>

<script>
import BaseImageViewerCloseButton from "./BaseImageViewerCloseButton";
import BaseImageViewerSlider from "./BaseImageViewerSlider";
import BaseImageViewerZoomButton from "./BaseImageViewerZoomButton";

import "viewerjs/dist/viewer.css";
import Viewer from "viewerjs";

export default {
  name: "BaseImageViewerImage",
  props: {
    images: {
      type: Array,
      required: true,
    },
  },
  components: {
    BaseImageViewerCloseButton,
    BaseImageViewerSlider,
    BaseImageViewerZoomButton,
  },
  data() {
    return {
      image: "",
      showModal: false,
      viewer: "",
      zoom: {
        number: 0,
        type: "",
      },
      config: {
        button: false,
        loading: true,
        navbar: false,
        toggleOnDblclick: true,
        zoomable: true,
        zoomOnTouch: true,
        zoomOnWheel: true,
        inline: false,
        backdrop: false,
        focus: false,
        fullscreen: false,
        loop: false,
        keyboard: false,
        movable: true,
        rotatable: false,
        scalable: false,
        slideOnTouch: false,
        title: false,
        toolbar: false,
        tooltip: true,
        transition: false,
        minZoomRatio: 1,
        maxZoomRatio: 10,
      },
    };
  },
  computed: {
    isValid() {
      return !!this.images.length;
    },
    imageUrl() {
      return this.image.img || "";
    },
  },
  methods: {
    changeZoom(value) {
      this.zoom = value;
    },
    selectImage() {
      this.mountViewer();
      this.disableZoomLessButton = true;
      this.showModal = true;
    },
    fechar() {
      this.viewer.destroy();
      this.disableZoomLessButton = false;
      this.showModal = false;
    },
    changeImage(imageIndex) {
      this.viewer.view(imageIndex);
    },
    changeImagePrevNext(type) {
      if (type === "prev") {
        this.viewer.prev();
      } else {
        this.viewer.next();
      }
    },
    getImage(value) {
      const img = this.images.filter((item) => item.id === this.imageId)[0];

      this.image = img;
    },
    mountViewer() {
      const imageRef = this.$refs.images;

      if (imageRef) {
        const viewerConfig = this.config;

        this.viewer = new Viewer(imageRef, {
          ...viewerConfig,
          viewed() {
            // console.log("oi");
            // _.viewer.zoomTo(30);
            // this.viewer.show();
            this.viewer.toggle();
          },
        });
      }
    },
  },
  watch: {
    imageId(value) {
      this.getImage(value);
    },
    zoom: {
      deep: true,
      immediate: true,
      handler(value) {
        if (value.type) {
          console.log("watch zoomIn -> ", value);
          let ratio = 0.1;

          if (value.type !== "plus") {
            ratio = -0.1;
          }

          console.log("--> ", ratio);
          this.viewer.zoom(ratio);
        }
      },
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.base-image-viewer {
  position: relative;
  list-style-type: none;
}
.viewer-container {
  z-index: 90001 !important;
  display: inline-block !important;
}
.base-image-tools {
  position: absolute !important;
  display: block;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 90001;
  background: black;
}
.base-image-tools-itens {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 90002;
}
</style>
