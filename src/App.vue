<template>
  <div id="app">
    <landing v-if="showDashboard" @LAUNCH_DASHBOARD='toggleScreen' :playersConnected="playersConnected" :chatroomId="chatroomId"/>
    <Dashboard v-else @LAUNCH_LANDING='toggleScreen' :playersConnected="playersConnected" :chatroomId="chatroomId" :users="users"/>
  </div>
</template>

<script>
import Dashboard from './components/Dashboard'
import Landing from './components/Landing'
import io from 'socket.io-client'

export default {
  name: 'App',
  components: {
    Dashboard,
    Landing
  },
  data () {
    return {
      showDashboard: true,
      playersConnected: 0,
      users: [],
      chatroomId: 'FETCHING'
    }
  },
  methods: {
    toggleScreen () {
      this.showDashboard = !this.showDashboard
    },
    emulateKeyPress (keyCode) {
      document.dispatchEvent(new KeyboardEvent('keydown', { keyCode }))
    }
  },
  mounted () {
    const vm = this
    const urlString = window.location.href
    const socket = io(urlString.split('7777')[0] + '7777')
    socket.on('connect', function () {
      console.log('Connecting to NoServer')
      if (urlString.split('=')[1]) {
        socket.emit('CONSOLE_REDIRECT', { sessionId: (urlString.split('=')[1]).split('&')[0], layout: 2 })
        vm.chatroomId = (urlString.split('=')[1]).split('&')[0]
      } else {
        socket.emit('CONSOLE_START_UP')
      }
    })

    socket.on('SET_SESSION_ID', function (res) {
      vm.chatroomId = res.data.sessionsId
    })

    socket.on('STATUS_INFO', function (res) {
      vm.playersConnected = res.playerCount
      console.log(res)
    })

    socket.on('CONTROL_INFO', function (res) {
      console.log(res)
      vm.emulateKeyPress(res.keyCode)
    })
  }
}
</script>

<style>
*, *::after, *::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 10px;
  height: 100%;
  width: 100%;
  background-color: #1e1e1f
}

body {
  height: 100%;
  width: 100%;
}

#app {
  height: 100%;
  width: 100%;
  background-color: #1e1e1f
}
</style>
