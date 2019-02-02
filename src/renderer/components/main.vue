<template>
  <div id="main">
    <div id="client">
      <iframe id="game" :src="gameurl" frameborder="0"></iframe>
    </div>
    <div id="tools">
      <div id="goHome" class="bar" @click="goHomeAction()">
        <i class="fa fa-home"></i>
      </div>
      <div id="setVolume" class="bar" @click="setVolumeAction()">
        <i :class="volume"></i>
      </div>
      <div id="showAbout" class="bar" @click="showAboutAction()">
        <i class="fa fa-warning"></i>
      </div>
      <v-dialog/>
    </div>
  </div>
</template>

<script>
  const {ipcRenderer: ipc} = require('electron')
  export default {
    name: 'main',
    data () {
      return {
        gameurl: 'https://majsoul.union-game.com/0/',
        volume: 'fa fa-volume-up'
      }
    },
    methods: {
      goHomeAction: function () {
        this.$modal.show('dialog', {
          title: '温馨提示',
          text: '请再次确认，您是否真的需要返回首页？',
          buttons: [
            {
              title: '确认',
              handler: () => {
                this.gameurl = 'https://majsoul.union-game.com/0/?rseed=' + Math.random()
                this.$modal.hide('dialog')
              }
            },
            {
              title: '取消'
            }
          ]
        })
      },
      setVolumeAction: function () {
        if (this.volume === 'fa fa-volume-up') {
          this.volume = 'fa fa-volume-off'
          ipc.send('mute')
        } else {
          document.getElementById('game').muted = false
          this.volume = 'fa fa-volume-up'
          ipc.send('unmute')
        }
      },
      showAboutAction: function () {
        this.$modal.show('dialog', {
          title: '注意',
          text: '这不是官方发布的雀魂客户端，而是由 @幻奏 制作的，该客户端使用 Electron 编写，所有代码您均可前往 Github 中查看。作者 Github 地址： https://github.com/illyasviels 。',
          buttons: [
            {
              title: '我已知晓'
            }
          ]
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  #main {
    position: relative;
    width: 100%;
    height: 100%;
    #client {
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: 9;
      iframe {
        width: 100%;
        height: 100%;
      }
    }
    #tools {
      position: absolute;
      width: 100%;
      height: 100%;
      .bar {
        position: absolute;
        color: white;
        font-size: 18px;
        padding: 8px;
        z-index: 19;
        &:hover {
          color: lightblue;
        }
      }
      #goHome {
        left: 10px;
        bottom: 8px;
      }
      #setVolume {
        left: 42px;
        bottom: 8px;
      }
      #showAbout {
        left: 74px;
        bottom: 8px;
      }
    }
  }
</style>
