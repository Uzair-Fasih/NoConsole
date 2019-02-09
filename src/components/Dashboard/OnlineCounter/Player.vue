<template>
  <div class="player" :style="{ backgroundColor: randomColor() }">
    <p class="player-initials">{{ getInititals(name) }}</p>
  </div>
</template>

<script>
export default {
  props: ['name'],
  methods: {
    randomColor () {
      return '#000000'.replace(/0/g, function () { return (~~(Math.random() * 16)).toString(16) })
    },
    getInititals (name) {
      let initials = name.match(/\b\w/g) || []
      initials = ((initials.shift() || '') + (initials.pop() || '')).toUpperCase()
      return initials
    }
  }
}
</script>

<style scoped>
.player {
  height: 8em;
  width: 8em;
  border-radius: 100%;
  background-color: #212121;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-right: 3em;
  border: .5em solid #212121;
}
.player-initials {
  text-align: center;
  font-family: sans-serif;
  font-size: 3em;
  color: #FFF;
}
</style>
