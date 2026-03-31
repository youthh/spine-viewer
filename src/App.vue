<template>
  <div id="app">
    <el-container id="main-container">
      <el-container>
        <el-main>
          <app-redirect-notice url="https://andryuha-ka.github.io/spineviewer/" :delay="10000" />
          <the-preview-stage />
        </el-main>
      </el-container>
      <the-side-panel/>
    </el-container>
  </div>
</template>

<script>

import ThePreviewStage from './components/ThePreviewStage.vue';
import TheSidePanel from './components/TheSidePanel.vue';
import AppRedirectNotice from './components/Redirect.vue';

export default {
  name: 'app',
  components: {
    TheSidePanel,
    ThePreviewStage,
    AppRedirectNotice,
  },
};
</script>

<style lang="scss">
html, body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  width: 100%;
  height: 100%;
}

#main-container {
  height: 100%;
  .el-main {
    //overflow: hidden;
    padding: 0;
  }
  /*
  .el-aside {
    padding: 20px;
  }*/
}

.el-input-number--mini {
  width: 110px!important;
}

.el-cascader-menu {
  max-height: 50vh;
}
</style>
