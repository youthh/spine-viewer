<template>
  <el-collapse-item>
    <div slot="title">
      <i class="el-icon-picture"></i>&nbsp;
      <b class="panel-group-title">Stage</b>
    </div>
    <el-form
      size="mini"
      label-width="100px"
    >

      <el-form-item label="Picture">
        <app-image-resource
          id="bgImage"
          size="small"
          :img-src="stageImgData"
          :img-filename="stageImgFile"

          @onChange="$_handleSceneImageChange"
          @onReset="$_handleSceneImageDelete"
        />
      </el-form-item>

    </el-form>
  </el-collapse-item>
</template>

<script>

import { RENDERER_TYPE, utils } from 'pixi.js';
import { mapGetters } from 'vuex';
import { stageImgData, stageImgFile } from '@/store/getters';
import AppImageResource from './AppImageResource.vue';

export default {
  name: 'TheSidePanelStageProps',
  components: {
    AppImageResource,
  },
  computed: {
    webGLNotSupported() {
      return !utils.isWebGLSupported();
    },
    renderType: {
      get() {
        if (this.webGLNotSupported) return 'Canvas2D';

        return this.$store.getters.stageRenderType === RENDERER_TYPE.WEBGL ? 'WebGL' : 'Canvas2d';
      },
      set(type) {
        this.$store.commit(
          'changeRenderType',
          type === 'WebGL' ? RENDERER_TYPE.WEBGL : RENDERER_TYPE.CANVAS,
        );
      },
    },
    bgColor: {
      get() {
        return this.$store.getters.stageColor;
      },
      set(v) {
        this.$store.commit('changeStageColor', v);
      },
    },
    zoom: {
      get() {
        return this.$store.getters.zoom;
      },
      set(v) {
        this.$store.commit('setZoom', v);
      },
    },
    posX: {
      get() {
        return this.$store.getters.pos.x;
      },
      set(x) {
        this.$store.commit('changeImgPos', {
          x,
          y: this.posY,
        });
      },
    },
    posY: {
      get() {
        return this.$store.getters.pos.y;
      },
      set(y) {
        this.$store.commit('changeImgPos', {
          y,
          x: this.posX,
        });
      },
    },
    ...mapGetters([
      'stageImgFile',
      'stageImgData',
    ]),
  },
  methods: {
    stageImgFile,
    stageImgData,
    $_handleSceneImageDelete() {
      this.$store.commit('changeStageImg', {
        fileData: '',
        filename: '',
      });
    },
    $_handleSceneImageChange(fileData, filename) {
      this.$store.commit('changeStageImg', {
        fileData,
        filename,
      });
    },
  },
};
</script>

<style scoped>

</style>
