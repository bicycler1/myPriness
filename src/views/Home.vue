<template>
  <div>
    <div class="w-100 vh-100 container-me">
      <div class="warp w-100">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
        <img class="vw-100 vh-100" src="@/assets/HomeImgs/photos1.jpg" alt="">
      </div>
    </div>
    <div class="list-dot">
      <li class="circle circle-border" listId="0" @click="listChoose($event)"></li>
      <li class="circle circle-border" listId="1" @click="listChoose($event)"></li>
      <li class="circle circle-border" listId="2" @click="listChoose($event)"></li>
      <li class="circle circle-border" listId="3"></li>
      <li class="circle circle-border" listId="4"></li>
      <li class="circle circle-border" listId="5"></li>
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
  right: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  padding: 6px;
  height: 110px;
}
.circle{
  width: 8px;
  height: 8px;
  border-radius: 50%;
  cursor: pointer;
}
.circle-border{
  border: 1px solid #eee;
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
      photoPosition: 0
    }
  },
  methods: {
    nextPhoto: function () {
      this.photoPosition++
      if (this.photoPosition === 5) {
        $('.next-icon').hide(1000)
      }
      $('.warp').animate({
        top: -this.photoPosition * 100 + '%'
      }, 1000)
    },
    listChoose: function (event) {
      this.photoPosition = $(event.target).attr('listId')
      let listDot=$('.circle')
      for(let i=0;i<listDot.length;i++){
        $(listDot[i]).removeClass('circle-click')
        $(listDot[i]).addClass('circle-border')
      }
      $(event.target).removeClass('circle-border')
      $(event.target).addClass('circle-click')
      if (this.photoPosition === 5) {
        $('.next-icon').hide(1000)
      }
      $('.warp').animate({
        top: -this.photoPosition * 100 + '%'
      }, 1000)
    },
    init: function () {
      if (this.photoPosition === 0) {
        $('.pre-icon').fadeToggle(1000)
      }
    }
  },
  mounted: function () {
    this.init()
  }
}
</script>
