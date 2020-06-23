<template>
  <div class="horizontal-picker">
    <div style="position: relative">
      <!--{List}}-->
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div class="swiper-slide"  v-for="(item, index) in list" :key="index">  {{item.text}}</div>
        </div>
        <div class="swiper-slide-static-active"></div>
        <!-- Add Pagination -->
        <div class="swiper-pagination"></div>
      </div>
      <div class="swiper-button-next"></div>
      <div class="swiper-button-prev"></div>
    </div>
  </div>
</template>

<script>
  import 'swiper/css/swiper.css'
  import Swiper from  'swiper/js/swiper'
  import './HorizontalPicker.css'
  export default {
    name: "daysSelect",
    data(){
      return{
        productDetailsText:{},
        nums:[1,2,3,4,5,6,7,8,9,10],
        activeSlide:0,
        HPicker:null,
        inClick: false,
      }
    },
    props:['list', 'value'],
    mounted(){
      this.init();
    },
    methods:{
      init(){
       let _this = this;

        this.HPicker = new Swiper('.swiper-container', {
          slidesPerGroup:1,
          observer:true,
          observeParents:true,
          centeredSlides : true,
          slideToClickedSlide: true,
          watchSlidesProgress : true,
          speed:300,
          slidesPerView: 7,
          spaceBetween: -10,
          loop : true,
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev',
          },
          on: {
            init: function(){
              this.emit('transitionEnd');//在初始化时触发一次transitionEnd事件，需要先设置transitionEnd
            },
            transitionEnd: function(){
              _this.activeSlide = this.realIndex;
              _this.setValue();
              if(_this.HPicker) _this.update(_this.HPicker)
            },
          },
        });
        if(_this.value){
          _this.list.forEach((it,i)=>{
            if(it.value == _this.value){
              _this.HPicker.slideToLoop(i);
              return false
            }
          })
        }
        _this.setValue();
      },
      update(swiper){
        swiper.loopFix();
        this.$forceUpdate();
      },
      setValue(){
        this.$emit('input', this.list[this.activeSlide].value);
      },
    },

  }
</script>
>
