<template>
  <div class="photo">
    <div class="container" v-for="(path, cl) in info" :key="cl">
      <div :class="`box imgi ${status1} ${status2 + cl}`  " ref="path"><img :src="path"></div>
    </div>
  </div>
</template>
 
<style>
.container {
  width: 80%;
  height: 100%;
  margin: 80px 70px;
  position: relative;
}
 
.box {
  width: 210px;
  transition: 0.1s;
  height: 100%;
  -moz-transition: 1s;
  -webkit-transition: 1s;
  position: absolute;
}
 
img {
  width: 100%;
  padding: 10px 10px 15px 10px;
  border: 1px solid #ddd;
  /*position:absolute;  */
 
  z-index: 1;
}
 
.box:hover {
  -webkit-transform: rotate(0deg) !important;
  transform: scale(1.5) !important;
  -webkit-transform: scale(1.5) !important;
  box-shadow: 4px 4px 10px #ccc !important;
  -moz-box-shadow: 4px 4px 10px #ccc !important;
  -webkit-box-shadow: 4px 4px 10px #ccc !important;
  z-index: 1 !important;
 
}
 
.imgi {
  margin-left: 50%;
  top: 0px;
  left: 0px;
  -webkit-transform: rotate(0deg);
}
 
.i {
  margin-left: 10%;
  top: 0px;
  left: 0px;
  -webkit-transform: rotate(0deg);
}
 
 
.img1 {
  margin-left: 50%;
  top: 250px;
  left: -700px;
  -webkit-transform: rotate(-40deg);
}
 
.img2 {
  top: 10px;
  left: -60px;
  -webkit-transform: rotate(-20deg);
}
 
.img3 {
  top: 0px;
  left: 600px;
  -webkit-transform: rotate(-20deg);
}
 
.img4 {
  top: 10px;
  left: 1100px;
  -webkit-transform: rotate(10deg);
}
 
.img5 {
  top: 300px;
  left: 600px;
  -webkit-transform: rotate(30deg);
}
 
.img6 {
  top: 10px;
  left: 800px;
  -webkit-transform: rotate(-10deg);
}
 
 
.img7 {
  top: 100px;
  left: 400px;
  -webkit-transform: rotate(20deg);
}
 
.img8 {
  top: 350px;
  left: 1050px;
  -webkit-transform: rotate(30deg);
}
 
.img9 {
  top: 200px;
  left: 900px;
  -webkit-transform: rotate(40deg);
}
 
.img10 {
  top: 200px;
  left: 1200px;
  -webkit-transform: rotate(50deg);
}
 
.img11 {
  top: 00px;
  left: 300px;
  -webkit-transform: rotate(50deg);
}
 
.img12 {
  top: 200px;
  left: 300px;
  -webkit-transform: rotate(50deg);
}
 
.img13 {
  top: 400px;
  left: 700px;
  -webkit-transform: rotate(-10deg);
}
 
.img14 {
  top: 300px;
  left: 250px;
  -webkit-transform: rotate(-30deg);
}
 
.img15 {
  top: 300px;
  left: 200px;
  -webkit-transform: rotate(40deg);
}
 
.img0 {
  top: 00px;
  left: 500px;
  -webkit-transform: rotate(0deg);
}
 
</style>
 
<script>
export default {
  name: "PhotoWall",
  data() {
    return {
      status1: '',
      status2: '',
      info: this.getList(),
    }
  },
  created() {
    this.getList()
    setTimeout(() => {
      this.status1 = 'i'
    }, 1000);
    setTimeout(() => {
      this.status2 = 'img'
    }, 1100)    //两个setTimeout，为了动态追加元素样式，增加点动效
  },
  methods: {
    getList() {
      this.p_l = { 'img1': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img2': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img3': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img4': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img5': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img6': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img7': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img8': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img9': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img10': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img11': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img12': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img13': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img14': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img15': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto', 'img16': 'https://img0.baidu.com/it/u=2261292692,2640661885&fm=26&fmt=auto' }    //这里可以使用数组，由于开始想复杂了，所以用了对象。
      var phono = []
      for (let i in this.p_l) {
        phono.push(this.p_l[i])    //获取照片
      }
      return phono
    }
  }
}
</script>