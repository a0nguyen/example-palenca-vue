<template>
  <div>
    <iframe
      :src="widgetUrl"
      style="width:100%;border:none;height:100vh"
    ></iframe>
  </div>
</template>

<script>
import io from 'socket.io-client'

export default {
  name: 'Home',
  data () {
    return {
      widgetUrl: 'https://www.palenca.com/form/759c55b3', // this is a demo widget, use your widget url
      socket: undefined
    }
  },
  created () {
    this.socket = io('https://socket.palenca.com/')
  },
  mounted () {
    this.socket.on('data', (content) => this.onData(content))
  },
  beforeDestroy () {
    this.socket.off('data')
  },
  methods: {
    onData (content) {
      const { user, platform } = content
      console.log(`user with id ${user} conected with ${platform} `) // do something with the data
      this.$router.push('thank-you')
    }
  }
}
</script>
