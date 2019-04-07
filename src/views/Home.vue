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
      globalValues: {
        timer: null,
        begin: null,
        durationNumber: 0,
        number: 0
      }
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
      if (delta < 0) {
        if (this.photoPosition === 5) {

        } else {
          this.nextPhoto()
          this.listDotStyle(this.photoPosition)
        }
      } else if (delta > 0) {
        if (this.photoPosition === 0) {

        } else {
          this.prePhoto()
          this.listDotStyle(this.photoPosition)
        }
      }
    },
    throttle: function (method, text, delay, duration) {
      let _this = this
      return function () {
        clearTimeout(_this.globalValues.timer)
        let current = new Date()
        console.log(_this.globalValues.begin)
        if (current - _this.globalValues.begin >= duration) {
          _this.globalValues.begin = current
          _this.globalValues.durationNumber++
          method(text)
        } else {
          if (_this.globalValues.durationNumber) {
            _this.globalValues.number++
            if (_this.globalValues.number <= 2) {

            } else {
              _this.globalValues.timer = setTimeout(function () {
                method(text)
              }, delay)
              _this.globalValues.durationNumber = 0
            }
          }
        }
      }
    }
  },
  mounted: function () {
    let _this = this
    this.globalValues.begin = new Date()
    $(document).mousewheel(function (event, delta) {
      _this.throttle(_this.mouseRoll, delta, 300, 1300)()
    })
  }
}
</script>
