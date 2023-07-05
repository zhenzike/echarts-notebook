<template>
   <div class="contentBox">
      <detailData class="firstBox" :barData="barMap" />
      <myMap  class="twoBox"/>
   </div>
</template>
<script>
import detailData from './detailData/detailData.vue'
import myMap from './map/myMap.vue'
export default {
   name: '',
   components: {
      detailData,
      myMap
   },
   mixins: [],
   props: {

   },
   data() {
      return {
         barMap:{
            '工作站数':80,
            '提醒次数':50,
            '调阅次数':55,
            '互认次数':78,
            '节省费用':64,
         }
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
.contentBox{
   display: flex;
   flex-direction: column;
   box-sizing: border-box;
   .firstBox{
      flex: 1;
      box-shadow: 0 0 2px 1px rgb(33, 76, 230),
      0 0 2px 1px rgb(33, 76, 230) inset;
      padding: 0.5rem;
   }
   .twoBox{
      flex: 2;
      padding: 0.5rem;
      margin-top: 0.5rem;
      box-sizing: border-box;
      // box-shadow: 0 0 2px 1px rgb(33, 76, 230),
      // 0 0 2px 1px rgb(33, 76, 230) inset;
   }
}
</style>