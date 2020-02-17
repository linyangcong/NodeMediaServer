<template>
  <div :class="appFlag?'PlayMain_app':'PlayMain'">
      <div class="PlayTop">
        <div>
          <video id="videoElement" width="100%" :height="appFlag?'':'450px'" controls="controls"></video>
          <div class="Play_danmu">
           <div>
             <span style="font-size:0.8rem">弹幕</span>
             <el-switch
             :size="appFlag?'mini':'small'"
             v-model="OpentheScroll"
             active-color="#f90"
             inactive-color="#666"
             ></el-switch>
           </div>
            <div class="danmuinput">
              <el-input :size="appFlag?'mini':'small'"  style="width:88%" v-model="danmuContent" :placeholder="loginflag&&OpentheScroll?danmu:danmuUnlogin" :disable="loginflag"></el-input>
              <el-button :size="appFlag?'mini':'small'"  type='warning' :disable="loginflag&&OpentheScroll">发送</el-button>
            </div>
          </div>
        </div>
        <div class="PlayItemPanel" v-show="!appFlag">
          <div class="PlayItem" v-for="(k,i) in playList" :key="i">
            <div><img :src="k.image" class="PlayItem_img" /></div>
            <div>
              <div style="font-size:14px">{{k.name}}</div>
              <div class="PlayItem_author">
                <span>{{k.author}}</span>
                <span>{{k.Time}}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

  </div>
</template>

<script>
import { resourceConfig ,server } from "../../resourceConfig";
export default {
  name: "HelloWorld",
  data() {
    return {
      // Year:new Date().getFullYear(),
      // month:new Date().getMonth(),
      // DateTime:new Date().getDate(),
      // msg: 'Welcome to Your Vue.js App'
      appFlag:false,
      OpentheScroll:false,
      danmu:'发条弹幕刷下存在感吧',
      danmuUnlogin:'要发弹幕，请先登录或注册',
      loginflag:false,
      danmuContent:'',
      playList: [
        {
          image: `${resourceConfig}/WebView/User/u1.jpg`,
          name: "大司马吃鸡111",
          author: "芜湖大司马1",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u2.jpg`,
          name: "大司马吃鸡222",
          author: "芜湖大司马2",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u3.jpg`,
          name: "大司马吃鸡333",
          author: "芜湖大司马3",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u1.jpg`,
          name: "大司马吃鸡111",
          author: "芜湖大司马1",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u2.jpg`,
          name: "大司马吃鸡222",
          author: "芜湖大司马2",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u3.jpg`,
          name: "大司马吃鸡333",
          author: "芜湖大司马3",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u3.jpg`,
          name: "大司马吃鸡333",
          author: "芜湖大司马3",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u1.jpg`,
          name: "大司马吃鸡111",
          author: "芜湖大司马1",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u2.jpg`,
          name: "大司马吃鸡222",
          author: "芜湖大司马2",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        },
        {
          image: `${resourceConfig}/WebView/User/u3.jpg`,
          name: "大司马吃鸡333",
          author: "芜湖大司马3",
          Time: `${new Date().getFullYear()}.${new Date().getMonth()}.${new Date().getDate()}`
        }
      ]
    };
  },
  mounted() {
    if(window.location.search){
    let name=window.location.search.split('?')[1].split('=')[0]
    let value=window.location.search.split('?')[1].split('=')[1]
    console.log(name,value)
    if(name='type'&&value=='app'){
      this.appFlag=true;
    }
    }
    
    if (flvjs.isSupported()) {
      var videoElement = document.getElementById("videoElement");
      var flvPlayer = flvjs.createPlayer({
        type: "flv",
        url: server+"/live/wangmin.flv"
        // url:'https://linyangcong.github.io/NodeMediaServer/live/wangmin.flv'
      });
      flvPlayer.attachMediaElement(videoElement);
      flvPlayer.load();
      flvPlayer.play();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.PlayMain {
  margin-left: 10%;
  width: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.PlayMain_app{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.PlayTop{
  display:flex;
  flex-direction:row;
  justify-content: space-between
}
.PlayItemPanel{
  width:40%;
  height:500px;
  overflow-y: scroll;
  overflow-x: hidden
}
.PlayItem{
  display:flex;
  flex-direction:row;
  padding: 5px;

  /* justify-content: space-between; */
  /* margin-top: 0.5rem; */
}
.PlayItem:hover{
  cursor: pointer;
  background: #acc
}
.PlayItem_img{
  width:120px;
  height:60px;
  border: 1px solid #eaa;
  border-radius: 10px;
}
.PlayItem_author{
display:flex;
flex-direction:row;
justify-content: space-between;
font-size: 12px;
color: #bbb
}
.Play_danmu{
  display: flex;
  flex-direction: row;
  padding: 10px;
  align-items: center;
  justify-content: space-between
}
.danmuinput{
  display: flex;
  flex-direction: row
}
</style>
