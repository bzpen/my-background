
<script setup lang="ts">
import { onMounted, ref } from 'vue';

const canvas = ref()

const diamond = ref({
  listWidth: [Number],
  listHeight: [Number],
  width: 100,
  height: 100,
  innerHeight: window.innerHeight,
  innerWidth: window.innerWidth
})

onMounted(() => {
  getDiamond()
})


/**
 * 根据页面大小获取菱形所需数量
 */
function getDiamond(){
  let height = window.innerHeight + 200
  let width = window.innerWidth
  diamond.value.listWidth = new Array(Math.ceil(width / diamond.value.width) + 1).fill(1)
  diamond.value.listHeight = new Array(Math.ceil(height / diamond.value.height) + 1).fill(1)
  console.log(diamond.value);
}


</script>

<template>
  <div class="bg">
    <div class="circle-bg">
      <div class="circle"></div>
    </div>
    <div class="content" v-for="(item, index) in diamond.listHeight" :key="index" :class="{ dislocation: (index) % 2 == 1 }">
      <div class="diamond" v-for="(item, index) in diamond.listWidth" :key="index">
      </div>
    </div>
  </div>
</template>

<style scoped lang="less">

.circle-bg{
  position: absolute;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
}

@keyframes slidein {
  0% {
    width: 100px;
    height: 100px;
  }
  50%{
    width: 800px;
    height: 800px;
  }
  100% {
    width: 0px;
    height: 0px;
  }
}

.circle{
  margin: 0px auto;
  width: 600px;
  height: 600px;
  background-image: url("../assets/background.png");
  background-size: 100% 100%;
  animation-duration: 3s;
  animation-name: slidein;
  // 重复动画
  animation-iteration-count: infinite;
}

.bg{
  /* position: relative; */
  /* top: -106px; */
  width: 100%;
  height: 100vh;
  position: fixed;
  top:0px;
  left: 0px;
  background-color: #000000;
}

.dislocation {
  position: relative;
  left: -50px;
}

.content {
  display: flex;
  flex: initial;
  margin-top: 25px;
  position: relative;
  top: -106px;
}

.diamond {
  display: inline-block;
  min-width: 100px;
  height: 55px;
  background: rgb(43, 29, 9);
  position: relative;
  top: 25px;
  margin: 1px;
  cursor: pointer;


  &::before{
    content: '';
    position: absolute;
    top: -25px;
    left: 0;
    width: 0px;
    height: 0px;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 25px solid rgb(43, 29, 9);

  }
  &::after{
    content: "";
    position: absolute;
    bottom: -25px;
    left: 0px;
    width: 0px;
    height: 0px;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-top: 25px solid rgb(43, 29, 9);
  }

  &:hover{
    background-color: rgb(255, 230, 0);
    &::before{
      border-bottom: 25px solid rgb(255, 230, 0);
    }
    &::after{
      border-top: 25px solid rgb(255, 230, 0);
    }
  }
}

</style>
