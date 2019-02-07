<template>
  <div id="app">
    <landing v-if="showDashboard" @LAUNCH_DASHBOARD='toggleScreen' :playersConnected="playersConnected" :chatroomId="chatroomId"/>
    <Dashboard v-else @LAUNCH_LANDING='toggleScreen' :playersConnected="playersConnected" :chatroomId="chatroomId" :users="users"/>
  </div>
</template>

<script>
import Dashboard from './components/Dashboard'
import Landing from './components/Landing'
import io from 'socket.io-client';

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
      chatroomId: 'fetching'
    }
  },
  methods: {
    toggleScreen () {
      this.showDashboard = !this.showDashboard
    },
    emulateKeyPress (keyCode) {
      document.dispatchEvent(new KeyboardEvent('keydown',{ keyCode }));
    }
  },
  mounted () {
    this.chatroomId = '233415'
    const socket = io('http://192.168.43.80:7777')
    const vm = this
    socket.on('connect', function () {
      socket.emit('startup', { data: { user: 'screen', chatroomId: vm.chatroomId }});
    })
    socket.on('message', function (res) {
      vm.playersConnected = res.data.playersConnected
      vm.users = res.data.users
    })
    socket.on('control', function (res) {
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
