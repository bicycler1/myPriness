<template>
  <div>
    <div class="w-100 vh-100 container-me">
      <div class="warp w-100">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
      </div>
    </div>
    <div class="list-dot">
      <li class="circle circle-click" listId="0" @click="listChoose($event)"></li>
      <li class="circle circle-border" listId="1" @click="listChoose($event)"></li>
      <li class="circle circle-border" listId="2" @click="listChoose($event)"></li>
      <li class="circle circle-border" listId="3" @click="listChoose($event)">></li>
      <li class="circle circle-border" listId="4" @click="listChoose($event)">></li>
      <li class="circle circle-border" listId="5" @click="listChoose($event)">></li>
    </div>
    <div class="pre-icon">
      <i class="fa fa-chevron-up fa-4x"></i>
    </div>
    <div class="next-icon" @click="nextPhoto()">
      <i class="fa fa-chevron-down fa-4x"></i>
    </div>
  </div>
</template>

<style scoped>
  .container-me{
    position: relative;
    overflow: hidden;
  }
.warp{
  position: absolute;
  top: 0;
}
.list-dot{
  position: absolute;
  top: 50%;
  right: 6px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  padding: 6px;
  height: 200px;
}
.circle{
  width: 16px;
  height: 16px;
  border-radius: 50%;
  cursor: pointer;
}
.circle-border{
  border: 2px solid #eee;
}
.circle:hover{
  background: #3ac0ff;
}
  .circle-click{
    background: #3ac0ff;
  }
  .pre-icon{
    position: absolute;
    top: 0;
    left: 50%;
    display: none;
    padding: 16px;
    margin-left: -48px;
    transform: scale(1.2,0.9);
    opacity: 0.7;
  }
  .next-icon{
    position: absolute;
    bottom: 0;
    left: 50%;
    padding: 16px;
    margin-left: -48px;
    transform: scale(1.2,0.9);
    opacity: 0.7;
  }
</style>

<script>
// @ is an alias to /src
export default {
  name: 'home',
  data () {
    return {
      photoPosition: 0,
      timer: null
    }
  },
  methods: {
    nextPhoto: function () {
      this.photoPosition++
      if (this.photoPosition === 5) {
        $('.next-icon').fadeToggle(1000)
      }
      $('.warp').animate({
        top: -this.photoPosition * 100 + '%'
      }, 1000)
    },
    prePhoto: function () {
      this.photoPosition--
      $('.warp').animate({
        top: -this.photoPosition * 100 + '%'
      }, 1000)
    },
    listDotStyle: function (number) {
      let listDot = $('.circle')
      for (let i = 0; i < listDot.length; i++) {
        $(listDot[i]).removeClass('circle-click')
        $(listDot[i]).addClass('circle-border')
      }
      $(listDot[number]).removeClass('circle-border')
      $(listDot[number]).addClass('circle-click')
    },
    listChoose: function (event) {
      this.photoPosition = $(event.target).attr('listId')
      this.listDotStyle(this.photoPosition)
      if (this.photoPosition === 5) {
        $('.next-icon').fadeToggle(1000)
      }
      $('.warp').animate({
        top: -this.photoPosition * 100 + '%'
      }, 1000)
    },
    mouseRoll: function (delta) {
      let _this = this
      if (delta < 0) {
        if (_this.photoPosition === 5) {

        } else {
          _this.nextPhoto()
          _this.listDotStyle(this.photoPosition)
        }
      } else if (delta > 0) {
        if (_this.photoPosition === 0) {

        } else {
          _this.prePhoto()
          _this.listDotStyle(this.photoPosition)
        }
      }
    },
    throttle: function (method, text, delay, duration) {
      console.log(this.timer)
      let begin = new Date()
      let _this=this
      return function () {
        let context = this
        let current = new Date()
        clearTimeout(_this.timer)
        if (current - begin >= duration) {
          method.call(context, text)
          begin = current
        } else {
          console.log(_this.timer)
          _this.timer = setTimeout(function () {
            method.call(context, text)
          }, delay)
          console.log(_this.timer)
        }
      }
    }
  },
  mounted: function () {
    let _this = this
    $(document).mousewheel(function (event, delta) {
      console.log(delta)
      _this.throttle(_this.mouseRoll, delta, 500, 1000)()
    })
  }
}
</script>
