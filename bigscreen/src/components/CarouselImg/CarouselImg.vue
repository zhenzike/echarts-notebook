<template>
   <div class="CarouselImg">
      <h1 class="text">医院满意度数据</h1>
      <div class="myCarouselBox">
         <myCarousel :data="CarouselImgList" :class-option="classOption" :editYPos="editYPos" class="seamless-warp"
            ref="seamlessWarpUl">
            <ul>
               <li v-for="(item, index) in CarouselImgList" :key="index">
                  <p class="access-name">{{ item.city }}</p>
                  <p class="access-num">{{ item.joinRate || 0 }}%</p>
               </li>
            </ul>
         </myCarousel>
      </div>

   </div>
</template>
<script>
import myCarousel from './myCarousel.vue'
export default {
   name: '',
   components: {
      myCarousel
   },
   mixins: [],
   props: {
      CarouselImgList: {
         type: Array,
         default: []
      }
   },
   data() {
      return {
         classOption: {
            irection: 0,
            step: 0.25, // 数值越大速度滚动越快
            waitTime: 100,
            // autoPlay: false,
            //  step: 0.2, // 数值越大速度滚动越快
            //     limitMoveNum: 2, // 开始无缝滚动的数据量 this.dataList.length
            // hoverStop: true, // 是否开启鼠标悬停stop
            //     direction: 0, // 0向下 1向上 2向左 3向右
            //     openWatch: true, // 开启数据实时监控刷新dom
            //     singleHeight: 0, // 单步运动停止的高度(默认值0是无缝不停止的滚动) direction => 0/1
            //     singleWidth: 0, // 单步运动停止的宽度(默认值0是无缝不停止的滚动) direction => 2/3
            //     waitTime: 1000, // 单步运动停止的时间(默认值1000ms)
         },
         realBox: null,
         editYPos: 0,
      }
   },
   computed: {

   },
   watch: {

   },
   mounted() {
      // setTimeout(() => {
      //    this.realBox = this.$refs.seamlessWarpUl.$refs.realBox
      //    //当鼠标位于地区接入情况时，禁止网页滑动
      //    this.realBox.addEventListener('mouseover', function (e) {
      //       e.fromElement.onmousewheel = () => {
      //          return false
      //       }
      //    })
      //    this.realBox.addEventListener("wheel", this.wheelEvent);
      // }, 0)
   },
   methods: {
      // wheelEvent(e) {
      //    let commaIndex = this.realBox.style.transform.indexOf(',') + 1
      //    let transformY = this.realBox.style.transform.slice(commaIndex, -3) - 0
      //    if (e.wheelDelta > 0) {
      //       // console.log('向上滚动');
      //       this.realBox.style.transform = `translate(0px,${transformY - 12}px)`
      //       this.editYPos = transformY - 12
      //    } else {
      //       this.realBox.style.transform = `translate(0px,${transformY + 12}px)`
      //       this.editYPos = transformY + 12
      //       // console.log('向下滚动');
      //    }
      // }
   }
};
</script>
<style lang='scss' scoped>
.CarouselImg {
   display: flex;
   flex-direction: column;
   box-sizing: border-box;
   width: 100%;
   height: 100%;
   margin-top: 0.5rem;
   padding: 0.5rem;
   box-shadow: 0 0 2px 1px rgb(33, 76, 230),
      0 0 2px 1px rgb(33, 76, 230) inset;
   overflow: hidden;


   .text {
      flex: none;
      margin: 0;
      padding: 0 0 0.5rem 0;
      text-align: center;
      font-size: 1.5rem;
      font-weight: 600;
      color: rgb(2, 184, 231);
   }

   .myCarouselBox {
      flex: 1;
      overflow: hidden;
      padding: 0.5rem 0;
      .seamless-warp {
         box-sizing: border-box;
         width: 100%;
         height: 100%;



         ul {
            list-style: none;
            padding: 0;
            margin: 0 auto;

            li {
               display: flex;
               box-sizing: border-box;
               justify-content: space-between;
               font-size: 0.6rem;
               border-radius: 0.2rem;
               background: linear-gradient(to right, rgb(33, 66, 111), transparent);
               margin: 0.5rem 0;
               padding: 0 0.5rem;

               p {
                  color: white;
                  margin: 0;
                  height: 2rem;
                  line-height: 2rem;
               }
            }
         }

         ul li:first-child {
            margin-top: 0;
         }


      }
   }


}
</style>