<template>  
    <div class="slider_delete" :style="{'transform':'translateX(' + currentX + 'px)','-o-transform':'translateX(' + currentX + 'px)','-moz-transform':'translateX(' + currentX + 'px)','-webkit-transform':'translateX(' + currentX + 'px)'}"   
        @touchstart.stop="touchStart($event)"   
        @touchend.stop="touchEnd($event)"  
        @touchmove.stop="touchMove($event)" ref="container">  
        <slot></slot>  
    </div>  
</template>  
<script>
    /*
     * 滑动配置。distance 滑动距离
     */
    export default({
      data () {
        return {
          startPos: {x: 0, y: 0},
          endPos: {x: 0, y: 0},
          movePos: {x: 0, y: 0},
          currentX: 0
        }
      },
      props: ['sliderConf'],
      methods: {
        touchStart (e) {
          this.startPos.x = e.changedTouches[0].pageX
          this.startPos.y = e.changedTouches[0].pageY
        },
        touchMove (e) {
          var x = e.changedTouches[0].pageX
          var y = e.changedTouches[0].pageY
          var distance = this.sliderConf.distance
          // 横向位移大于纵向位移，阻止纵向滚动
          if (Math.abs(x - this.startPos.y) > Math.abs(y - this.startPos.x)) {
            return
          }
          // temp 将滑动距离
          var temp = (x - this.movePos.x)
          // 查询当前位置值
          if (temp < 0 && this.currentX > -distance) {
            this.currentX = this.currentX + temp
          }
          this.movePos.x = x
          e.preventDefault()
        },
        touchEnd (e) {
          var distance = this.sliderConf.distance
          this.endPos.x = e.changedTouches[0].pageX
          this.endPos.y = e.changedTouches[0].pageY
          var currenTransitionTime = 'transform 300ms'
          if (this.endPos.x - this.startPos.x < 0) {
            this.currentX = -distance
          } else if (this.endPos.x - this.startPos.x > 0) {
            this.currentX = 0
            this.setTransition(this.$refs.container, currenTransitionTime)
          }
          // 最后判断，如果超出最阀值，就还原
          if (this.currentX < -distance || this.currentX > 0) {
            this.currentX = 0
          }
        },
        setTransition (ele, val) {
          if (!ele) {
            return
          }
          ele.style.transition = val
          ele.style.WebkitTransition = '-webkit-' + val
          ele.style.MozTransition = '-moz-' + val
          ele.style.OTransition = '-o-' + val
        }
      }
    })
</script>
<style>
</style>
