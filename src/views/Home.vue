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
      <li class="circle" listId="0" @click="listChoose($event)"></li>
      <li class="circle" listId="1" @click="listChoose($event)"></li>
      <li class="circle" listId="2" @click="listChoose($event)"></li>
      <li class="circle" listId="3"></li>
      <li class="circle" listId="4"></li>
      <li class="circle" listId="5"></li>
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
  height: 90px;
}
.circle{
  width: 9px;
  height: 9px;
  border-radius: 50%;
  border: 1px solid #333;
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
