<template>
  <div class="header">
    <img id="logo" src="../../assets/icon.svg" />
    <div class="container">
        <div class="code-container">
          <img id="link-logo" src="../../assets/icons/link.svg" />
          <p id="code">    
            {{chatroomId}}
          </p>
        </div>
        <div class="code-container" @click="toggleFullScreen()">
          <img id="link-logo" src="../../assets/icons/fullscreen.svg" />
        </div>
    </div>  
  </div>
</template>

<script>
export default {
  props: ['chatroomId'],
  methods: {
    test () {
      console.log('test')
    },
    toggleFullScreen() {
      if ((document.fullScreenElement && document.fullScreenElement !== null) ||    
      (!document.mozFullScreen && !document.webkitIsFullScreen)) {
        if (document.documentElement.requestFullScreen) {  
          document.documentElement.requestFullScreen();  
        } else if (document.documentElement.mozRequestFullScreen) {  
          document.documentElement.mozRequestFullScreen();  
        } else if (document.documentElement.webkitRequestFullScreen) {  
          document.documentElement.webkitRequestFullScreen(Element.ALLOW_KEYBOARD_INPUT);  
        }  
      } else {  
        if (document.cancelFullScreen) {  
          document.cancelFullScreen();  
        } else if (document.mozCancelFullScreen) {  
          document.mozCancelFullScreen();  
        } else if (document.webkitCancelFullScreen) {  
          document.webkitCancelFullScreen();  
        }  
      }  
    }
  }
}
</script>


<style scoped>
.header {
  height: 6em;
  padding: 1em 2em;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  background-color: #2d2d2d;
}

#logo {
  height: 4em;
  align-self: center;
}

.container {
  display: flex;
  flex-direction: row;
  align-self: center;
  justify-content: space-between;
}

.code-container {
  display: flex;
  flex-direction: row;
  background-color: #1e1e1f;
  justify-content: space-around;
  padding: .5em 1em;
  border-radius: .2em ;
  margin-left: 1em;
}

#link-logo {
  height: 2em;
  align-self: center;
}

#code {
  color: #FFF;
  font-family: sans-serif;
  font-size: 2.5em;
  margin-left: .5em;
}
</style>

