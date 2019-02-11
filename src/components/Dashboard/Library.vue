/* eslint-disable */
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
          maxPlayers: 1,
          layout: 2
        },
        {
          title: 'Pacman',
          thumbnail: 'http://images6.fanpop.com/image/photos/39000000/Pac-Man-pac-man-39056094-1600-900.jpg',
          maxPlayers: 1,
          layout: 2
        },
        {
          title: 'Astray',
          thumbnail: 'https://superdevresources.com/wp-content/uploads/2014/09/astray-webgl-maze-game-open-source.jpg',
          maxPlayers: 1,
          layout: 2
        },
        {
          title: 'MortalKombat',
          thumbnail: 'https://superdevresources.com/wp-content/uploads/2014/09/mk-open-source-game.jpg',
          maxPlayers: 2,
          layout: 3
        },
        // {
        //   title: 'Hextris',
        //   thumbnail: 'https://games.tcdn.co/media/33/cover.jpg',
        //   maxPlayers: 1
        // }
      ]
    }
  },
  methods: {
    incrementSelected () {
      if (this.selected < this.games.length) {
        this.selected += 1
      }
    },
    decrementSelected () {
      if (this.selected > 1) {
        this.selected -= 1
      }
    },
    playGame () {
      window.location.href = `http://192.168.43.80:7777/Game/${this.games[this.selected - 1].title}/${this.chatroomId}/${this.games[this.selected - 1].layout}`
    },
    emulateKeyPress (keyCode) {
      document.dispatchEvent(new KeyboardEvent('keydown', { keyCode }))
    }
  },
  mounted () {
    const vm = this
    document.onkeydown = function (e) {
      e = e || window.event
      switch (e.which || e.keyCode) {
        case 37: vm.decrementSelected(); console.log('left'); break // Left
        case 39: vm.incrementSelected(); console.log('right'); break // right
        case 13: vm.playGame(); console.log('up'); break // up
        default:
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
