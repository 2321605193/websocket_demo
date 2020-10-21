<template>
  <div>
    <div>
      <input type="file">
    </div>
    <span>{{message}}</span>

    <button @click="goBriay">发送消息</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      message: '',
      ws: null
    }
  },

  mounted () {
    if(window.WebSocket){
    this.ws = new WebSocket('ws://localhost:8002');


      this.ws.onopen = (e) => {
        console.log("连接服务器成功");
        // 向服务器发送消息
        this.ws.send("what`s your name?");
      }
      this.ws.onclose = (e) =>{
        console.log("服务器关闭");
      }
      this.ws.onerror = () =>{
        console.log("连接出错");
      }
      // 接收服务器的消息
      this.ws.onmessage = (e) => {
        this.message = "message:"+e.data+"";

      }   
    }
  },

  methods: {
    goBriay () {
        var file = document.querySelector('input[type="file"]').files[0];
        this.ws.send(file);
    }
  }
}
</script>


<style scoped>

</style>
