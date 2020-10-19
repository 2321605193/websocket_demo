<template>
  <div>
    <span>{{message}}</span>

    <button @click="goBriay">二进制流</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      message: ''
    }
  },

  mounted () {
    let vm = this;
    if(window.WebSocket){
      var ws = new WebSocket('ws://localhost:8001');

      ws.onopen = function(e){
        console.log("连接服务器成功");
        // 向服务器发送消息
        ws.send("what`s your name?");
      }
      ws.onclose = function(e){
        console.log("服务器关闭");
      }
      ws.onerror = function(){
        console.log("连接出错");
      }
      // 接收服务器的消息
      ws.onmessage = function(e){
        vm.message = "message:"+e.data+"";
  
      }   
    }
  },

  methods: {
    goBriay () {
        this.$router.push('/test')
    }
  }
}
</script>


<style scoped>

</style>
