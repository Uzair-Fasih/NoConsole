/* eslint-disable */
<template>
  <div class="dashboard">
    <NoConsoleHeader :chatroomId="chatroomId"/>
    <OnlineCounter :users="users"/>
    <Library :chatroomId="chatroomId"/>
  </div>
</template>

<script>
import NoConsoleHeader from './Dashboard/Header'
import OnlineCounter from './Dashboard/OnlineCounter'
import Library from './Dashboard/Library'
export default {
  components: {
    NoConsoleHeader,
    OnlineCounter,
    Library
  },
  props: ['playersConnected', 'chatroomId', 'users'],
  watch: {
    playersConnected: function (n, o) {
      if (n === 0) {
        this.$emit('LAUNCH_LANDING')
      }
    }
  }
}
</script>

<style scoped>
.dashboard {
  display: flex;
  flex-direction: column;
}
</style>
