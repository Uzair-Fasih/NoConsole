/* eslint-disable */
<template>
  <div class="Landing">
    <img id="logo" src="../assets/icon.svg" />
    <p id="highlight">NoConsole</p>
    <p id="mediumlight">Connect using the following code</p>
    <div class="code-container">
      <img id="link-logo" src="../assets/icons/link.svg" />
      <p id='code'>
        {{ chatroomId }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['playersConnected', 'chatroomId'],
  watch: {
    playersConnected: function (n, o) {
      if (n !== 0) {
        this.$emit('LAUNCH_DASHBOARD')
      }
    }
  }
}
</script>

<style scoped>
.Landing {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

#logo {
  align-self: center;
}

#highlight, #mediumlight {
  text-align: center;
  color: #FFF;
  font-family: sans-serif;
  margin-top: 1em;
}

#highlight {
  font-size: 4em;
}

#mediumlight {
  font-size: 3em;
}

.code-container {
  display: flex;
  flex-direction: row;
  background-color: #2d2d2d;;
  padding: 1em 2em;
  border-radius: .2em ;
  margin-top: 5em;
  align-self: center;
}

#link-logo {
  height: 4em;
  align-self: center;
}

#code {
  color: #FFF;
  font-family: sans-serif;
  margin-left: .5em;
  font-size: 4em;
  font-weight: bold;
}
</style>
