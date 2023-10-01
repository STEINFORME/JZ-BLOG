<script setup>

</script>

<template >
  
  <div class="direction"  ref="sliderContainer" @touchstart="handleTouchStart" @touchmove="handleTouchMove" @touchend="handleTouchEnd" >
    <div class="zhezhao1" :style="{'animation': open == 1? 'welcomemove 2s  ease-in-out forwards': open == 0?'welcomeback 2s  ease-in-out forwards': ''}">
      <img src="./assets/JZ.png" class="JZLOGO">
      <div class="welcome">
    {{huanying}}
  </div>
  <img src="./img/arrow.png" class="arrow">
  </div>
 
    <div class="mengban1" :style="{'animation': Jzhankai ? ' chooseY 0.5s  ease-in-out both':'chooseN 0.5s ease-in-out both' }" v-on:mouseenter="  mengbanzhankai(1)">
  <div class="CIR1"></div>
  <div class="name">{{ name1 }}</div>
  <div class="login" @click="login(J)">登录</div>
  <div class="tourist" @click="tourist(J)">游客</div>
</div>
<div class="mengban2" :style="{'animation': Zzhankai ? 'chooseY 0.5s ease-in-out  both':'chooseN 0.5s ease-in-out both'}" v-on:mouseenter="  mengbanzhankai(2) ">
  <div class="CIR2"></div>
  <div class="name">{{ name2 }}</div>
  <div class="login" @click="login(Z)">登录</div>
  <div class="tourist" @click="tourist(Z)">游客</div>
</div>
</div>
  
 
</template>
<script>


import { defineComponent } from 'vue'

export default defineComponent({
  setup() {
    return{
      
    }
  },
  data(){
    return{
      initialText: 'Agnoi_ji & Z 欢迎您来到共同博客导航,请下滑滚轮进行选择. ',
      index: 0,
      huanying: '',
     open:'2',
      name1:'Agnoi_ji',
      name2:'Z',
      screenHeight:'',
      screenWidth:'',
      mengban1:'',
      mengban2:'',
      Jzhankai:false,
      Zzhankai:true,
      Jready:true,
      Zready:false,
      showchoose:false,
     
    }
  },
  mounted () {
     this.screenHeight = document.documentElement.clientHeight
     this.screenWidth= document.documentElement.clientWidth
     console.log(this.screenWidth)
 
     this.mengban1=this.screenWidth/2
     this.mengban2=this.screenWidth/2
    console.log(this.screenHeight)
    console.log(this.ready)
    window.addEventListener('wheel', this.handleMouseWheel, {
      passive: false,
    })
   
const TIME =setInterval(() => {
      if(this.index < this.initialText.length){
      this.autoTyping()
    }else{
      console.log('结束')
      clearInterval(TIME)
    }
    }, 100)
  
  },
  methods: {
    // 一段文字
    // 自增index
    // 展示
    // 临界值
    autoTyping () {
   
      this.index++
      this.huanying = this.initialText.slice(0, this.index)
   
  },
  handleTouchStart (e) {
      this.touchStartX = e.touches[0].pageX
      this.touchStartY = e.touches[0].pageY
    },
  handleTouchMove (e) {
      
      const touchCurrentY = e.touches[0].pageY
      if (touchCurrentY < this.touchStartY) {
        this.open=true
        console.log('用户向shang滑动')
      }
    },
  handleTouchEnd (e) {
      // 清空触摸起始位置
      this.touchStartX = null
    },
    handleMouseWheel(e) {
	if (!window.scrollY) {
		// 禁止页面滚动
		 e.preventDefault()
		
		if (e.wheelDelta) {
			// 判断浏览器IE，谷歌滑轮事件
      console.log(e.wheelDelta)
      
			if (e.wheelDelta > 0) {
        this.currentActive--
				console.log('向上移动')
        this.open=0
			}
			if (e.wheelDelta < 0) {
        this.currentActive++
				// 当滑轮向下滚动时
				console.log('向下移动')
       this.open=1
			}
		} 
    else if (e.detail) {
			// Firefox滑轮事件
			if (e.detail > 0) {
				// 当滑轮向下滚动时
        this.open=1
			}
			if (e.detail < 0) {
        this.currentActive--
				// 当滑轮向上滚动时
        this.open=0
			console.log('s2')
			}
		}
	}
},
beforeDestroy() {
    window.removeEventListener('wheel', this.handleMouseWheel, {
      passive: false,
    })},
    mengbanzhankai(a){
      console.log(a)
      if(a == 1){
        console.log(this.Jready)
        if(this.Jready){
       this.Jzhankai =true
       this.Zzhankai =false
       window.setTimeout(()=>{
       
        this.Zready=true
        this.Jready=false
       },400)
      }
        
      }else{
        console.log(this.Zready)
      if(this.Zready){
        this.Zzhankai =true
        this.Jzhankai =false
        window.setTimeout(()=>{
        this.Jready=true
        this.Zready=false
       },400)
      }
      }
       
      
    }


  }

  
})
</script>



