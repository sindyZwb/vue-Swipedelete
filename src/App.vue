<template>
  <div id="app">
    <Swipedelete :sliderConf="sliderConf">
      <div class="list">
        <div class="wrapper">
          <div class="content">content</div>
          <div class="del-btn">删除</div>
        </div>
      </div>
    </Swipedelete>
  </div>
</template>

<script>
import Swipedelete from './components/Swipedelete'

export default {
  name: 'app',
  components: {
    Swipedelete
  },
  data () {
    return {
      'sliderConf': {
        'distance': 60
      }
    }
  }
}
</script>
<style>
*{
   margin:0;
   padding:0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.list{
  height: 30px;
  border-bottom:1px solid #333;
  line-height: 30px;
  position: relative;
}
.list .del-btn{
  background:red;
  color:#fff;
  text-align: center;
  height:30px;
  line-height: 30px;
  width:60px;
  position: absolute;
  top:0;
  right:-60px;
}
</style>
