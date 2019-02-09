/* eslint-disable */
<template>
  <div class="game" :style="{ backgroundImage: 'url(\'' + gameinfo.thumbnail + '\')' }" :class="{ selected: (selected === (index + 1)) }">
    <div class="container">
      <p class=game-title>{{ gameinfo.title }}</p>
      <span class="player-info">
          <img class="icon" src="../../../assets/icons/player.svg" />
          1-{{gameinfo.maxPlayers}} Players
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: ['gameinfo', 'selected', 'index'],
  mounted () {
    console.log((this.selected === (this.index + 1)))
  }
}
</script>

<style scoped>
.game {
  height: 25em;
  width: 40em;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  background-color: brown;
  background-size: cover;
  margin-right: 5em;
  transition: 0.3s ease;
}

.selected {
  transform: scale(1.1);
  box-shadow: 0px 0px 20px #ffaa00;
}

.container {
  height: 10em;
  display: flex;
  flex-direction: column;
  background-color: rgba(0, 0, 0, 0.75);
  padding: 2em;
}

.game-title {
  font-family: sans-serif;
  font-size: 4em;
  color: #FFF;
  font-weight: bold;
}

.player-info {
  color: #FFF;
  font-family: sans-serif;
  font-size: 2em;
  display: flex;
  flex-direction: row;
}

.icon {
  height: 1em;
  align-self: center;
  margin-right: 1em;
}
</style>
