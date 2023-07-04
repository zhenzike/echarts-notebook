<template>
   <div class="leftBox">
      <div class="pieImgBox">
         <h1 class="text">医院检测数据</h1>
         <div class="pieImg">
            <pieImg :pieImgData="pieImgData" />
         </div>

      </div>
      <CarouselImg :CarouselImgList="CarouselImgList" class="CarouselImgBox" />
   </div>
</template>
<script>
import CarouselImg from '@/components/CarouselImg/CarouselImg.vue'
import pieImg from './pieImg/pieImg.vue'
export default {
   name: '',
   components: {
      CarouselImg,
      pieImg
   },
   props: {

   },
   data() {
      return {
         pieImgData: [
            { name: '出院率', value: 90 },
             { name: '住院率', value: 10 }
         ],
         CarouselImgList:[
              {city:'美利坚医院',joinRate:81},
              {city:'日本医院',joinRate:55},
              {city:'韩国医院',joinRate:77},
              {city:'俄罗斯医院',joinRate:68},
              {city:'中国医院',joinRate:78},
              {city:'英国医院',joinRate:45},
              {city:'意大利医院',joinRate:55},
              {city:'法国医院',joinRate:44},
              {city:'德国医院',joinRate:14},
              {city:'新加坡医院',joinRate:99},
      
         ]


      }
   },
   computed: {

   },
   watch: {

   },
   mounted() {

   },
   methods: {

   }
};
</script>
<style lang='scss' scoped>
.leftBox {
   display: flex;
   flex-direction: column;
   box-sizing: border-box;

   .pieImgBox {
      flex: 1;
      display: flex;
      flex-direction: column;
      box-sizing: border-box;
      box-shadow: 0 0 2px 1px rgb(33, 76, 230),
         0 0 2px 1px rgb(33, 76, 230) inset;

      padding: 0.5rem;

      .text {
         flex: none;
         margin: 0;
         padding: 0 0 0.5rem 0;
         text-align: center;
         font-size: 1.5rem;
         font-weight: 600;
         color: rgb(2, 184, 231);
      }

      .pieImg {
         flex: 1;
         display: flex;
         width: 100%;

      }
   }


   .CarouselImgBox {
      flex: 2;
   }
}
</style>