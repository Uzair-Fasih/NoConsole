<template>
  <div class="library">
    <Game v-for="game in games" :key="games.indexOf(game)" :gameinfo="game" :index="games.indexOf(game)" :selected="selected" />
  </div>  
</template>

<script>
import Game from './Library/Game'
export default {
  components: {
    Game
  },
  props: [ 'chatroomId' ],
  data () {
    return {
      selected: 1,
      games: [
        {
          title: '2048',
          thumbnail: 'https://lh3.googleusercontent.com/jK3nAwOD4DwFkG4NY_c8Q3Bkc0q_mNoo8g_OCZqoYuwIBrAIrdvObcgkrz41t-XigCg=w300-rw',
          maxPlayers: 2
        },
        {
          title: 'Youtube',
          thumbnail: 'https://3playmedia-wpengine.netdna-ssl.com/wp-content/uploads/blog-header-08-24-2018-youtube-1400x550.png',
          maxPlayers: '*'
        },
        {
          title: 'Hextris',
          thumbnail: 'https://games.tcdn.co/media/33/cover.jpg',
          maxPlayers: 1
        }
      ]
    }
  },
  methods: {
    incrementSelected () {
      if (this.selected < this.games.length)
        this.selected += 1
    },
    decrementSelected () {
      if (this.selected > 1)
        this.selected -= 1
    },
    playGame () {
      if (this.selected === 1) {
        window.location.href = "http://192.168.43.80:7777/Game/2048/" + this.chatroomId
      }
    },
    emulateKeyPress (keyCode) {
      document.dispatchEvent(new KeyboardEvent('keydown',{ keyCode }));
    }
  },
  mounted () {
    const vm = this
    document.onkeydown = function(e) {
      e = e || window.event;
      switch(e.which || e.keyCode) {
        case 37: vm.decrementSelected(); console.log('left'); break // Left
        case 39: vm.incrementSelected(); console.log('right'); break // right
        case 13: vm.playGame(); console.log('up'); break // up
        default: return;
      }
    }
  }
}
</script>

<style scoped>
.library {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  padding: 6em;
  overflow-y: scroll;
  height: calc(100vh - 22em);
}
</style>

