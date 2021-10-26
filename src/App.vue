<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Vue.js files three app</h1>
    <div class="explorer">
      <p>
        Полный путь до выбранного элемента:
      </p>
      <output name="selectedPath" ref="selectedPath" class="output">...</output>
      <files-three :data="filesThree"/>
    </div>
  </div>
</template>

<script>
import data from '../public/static/node_modules.json'

export default {
  name: 'App',
  components: {
    FilesThree: () => import('./components/FilesThree/FilesThree.vue')
  },
  provide() {
    return {
      showSelectedItemPath: this.showSelectedItemPath,
    }
  },
  data() {
    return {
      filesThree: data,
    }
  },
  methods: {
    showSelectedItemPath(pathToItem) {
      this.$refs.selectedPath.value = pathToItem
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.v-h {
  position: absolute;
  clip: rect(0 0 0 0);
  width: 1px;
  height: 1px;
  margin: -1px;
}
</style>
