<template>
  <div id="app">
    <div id="control" style="-webkit-app-region: drag">
      <img class="icon" src="https://majsoul.union-game.com/0/favicon.ico">
      <span class="title">雀魂客户端（非官方版）</span>
      <span class="minimize" @click="min()" style="-webkit-app-region: no-drag"></span>
      <span class="maximize" @click="max()" style="-webkit-app-region: no-drag"></span>
      <span class="close" @click="close()" style="-webkit-app-region: no-drag"></span>
    </div>
    <div id="box">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
  import { ipcRenderer } from 'electron'
  export default {
    name: 'majsoulclient',
    methods: {
      min: function () {
        ipcRenderer.send('min')
      },
      max: function () {
        ipcRenderer.send('max')
      },
      close: function () {
        ipcRenderer.send('close')
      }
    }
  }
</script>

<style lang="scss">
  /* CSS */
  * {
    margin: 0;
    padding: 0;
  }
  html, body, #app {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
  #control {
    width: 100vw;
    height: 32px;
    background-color: rgb(59, 64, 71);
    .icon {
      position: absolute;
      width: 16px;
      height: 16px;
      padding: 8px;
    }
    .title {
      position: absolute;
      left: 24px;
      font-family: "微软雅黑",serif;
      font-size: 12px;
      padding: 8px;
      color: rgb(143, 154, 158);
    }
    .minimize {
      position: absolute;
      right: 50px;
      margin: 10px;
      padding: 6px;
      border-radius: 100%;
      background-color: #28ca42;
      &:hover {
        background-color: #6bca7b;
      }
    }
    .maximize {
      position: absolute;
      right: 26px;
      margin: 10px;
      padding: 6px;
      border-radius: 100%;
      background-color: #ffbd2e;
      &:hover {
        background-color: #ffdf80;
      }
    }
    .close {
      position: absolute;
      right: 2px;
      margin: 10px;
      padding: 6px;
      border-radius: 100%;
      background-color: #ff5f58;
      &:hover {
        background-color: #ff827f;
      }
    }
  }
  #box {
    width: 100vw;
    height: calc(100vh - 32px);
  }
</style>
