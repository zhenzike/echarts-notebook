<template>
   <div class="detailDataBox">
      <div class="text">
         <h1>数据统计<span>&nbsp;>>></span></h1>
      </div>
      <div class="BarBox">
         <div class="barMap"></div>
      </div>
   </div>
</template>
<script>
import * as echarts from 'echarts'

export default {
   name: '',
   components: {

   },
   mixins: [],
   props: {
       barData:{
         type:Object,
         default:()=>({})
       }
   },
   data() {
      return {
         Xtext:[],
         Yvlaue:[]
      }
   },
   computed: {

   },
   watch: {

   },

   created(){
      
   },
   mounted() {
      this.getBarData(this.barData)
      this.showBarMap(this.Xtext,this.Yvlaue)
   },
   methods: {
      showBarMap(Xtext,Yvlaue) {
         let mCharts = echarts.init(document.querySelector('.barMap'))
         let option = {
            xAxis: {
               type: 'category',
               data:Xtext
            },
            yAxis: {
               type: 'value',
            },
            series: [
               {
                  name: '数据',
                  type: 'bar',
                  data:Yvlaue
               }
            ],
            color:['rgb(9,241,116)'],
            grid:{          
               top:20,
               bottom:20,
               left:40,
               right:20,
               x:0,
               y:0
            }
         }

         mCharts.setOption(option)
      },

      getBarData(barData){
         for(let k in barData){
         this.Xtext.push(k)
         this.Yvlaue.push(barData[k])
      }
      }
   }
};
</script>
<style lang='scss' scoped>
.detailDataBox {
   display: flex;
   flex-direction: column;

   .text {
      flex: none;

      h1 {
         width: 12rem;
         padding-left: 1rem;
         font-size: 1.2rem;
         margin: -6px 0 0 -6px;

         background: linear-gradient(to right, rgb(254, 236, 0), transparent);

         span {
            background: linear-gradient(to right, #000, transparent);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
         }
      }
   }

   .BarBox {
      flex: auto;
      width: 100%;
      

      .barMap {
        margin: auto;
         width: 100%;
         height: 100%;
      }
   }

}
</style>