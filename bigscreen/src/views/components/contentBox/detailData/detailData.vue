<template>
   <div class="detailDataBox">
      <div class="text">
         <h1>数据统计<span>&nbsp;>>></span></h1>
      </div>
      <div class="BarBox">
         <div class="barMap"></div>
         <div class="lineMap"></div>
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
      barData: {
         type: Object,
         default: () => ({})
      },
      lineMap: {
         type: Object,
         default: () => ({})
      }
   },
   data() {
      return {
         Xtext: [],
         Yvlaue: []
      }
   },
   computed: {

   },
   watch: {

   },

   created() {

   },
   mounted() {
      this.showBarMap(this.getBarData(this.barData))
      this.showLineMap(this.getBarData(this.lineMap))
   },
   methods: {
      showBarMap(data) {
         let mCharts = echarts.init(document.querySelector('.barMap'))
         let option = {
            title: {
               text: '数据总量',
               left: 'center',
               textStyle: {
                  color: 'rgb(240,230,8)'
               }
            },
            xAxis: {
               type: 'category',
               data: data.Xtext,
               // splitLine: {
               //    show: false
               // },
            },
            yAxis: {
               type: 'value',
               splitLine: {
                  show: false
               },
               axisTick: {
                  show: true // 设置刻度线显示
               },
               axisLine: {
                  show: true // 设置轴线显示
               },
            },
            series: [
               {
                  name: '数据',
                  type: 'bar',
                  data: data.Yvlaue,
               
               }
            ],
            color: ['rgb(9,241,116)'],
            grid: {
               top: 30,
               bottom: 20,
               left: 30,
               right: 5,
               x: 0,
               y: 0
            }
         }

         mCharts.setOption(option)
      },


      showLineMap(data) {
         let myLineCharts = echarts.init(document.querySelector('.lineMap'))
         let option = {
            title: {
               text: '住院趋势',
               left: 'center',
               textStyle: {
                  color: 'rgb(240,230,8)'
               }
            },
            xAxis: {
               type: 'category',
               data: data.Xtext
            },
            yAxis: {
               type: 'value',
               splitLine: {
                  show: false
               },
               axisTick: {
                  show: true // 设置刻度线显示
               },
               axisLine: {
                  show: true // 设置轴线显示
               },
            },
            grid: {
               top: 30,
               bottom: 20,
               left: 60,
               right: 15,
               x: 0,
               y: 0
            },
            series: [
               {
                  name: '语文',
                  type: 'line', //图标类型
                  smooth: true, // 变为曲线图
                  data: data.Yvlaue,
                  // markArea: {  //区域标注
                  //    data: [
                  //       [
                  //          {
                  //             xAxis: '一月'
                  //          },
                  //          {
                  //             xAxis: '二月'
                  //          }
                  //       ],
                  //       [
                  //          {
                  //             xAxis: '三月'
                  //          },
                  //          {
                  //             xAxis: '四月'
                  //          }
                  //       ]
                  //    ]
                  // }
                  lineStyle: {
                     color: 'rgb(1,155,219)' // 设置折线颜色为蓝色
                  },
               },
            ]

         }

         myLineCharts.setOption(option)

      },

      getBarData(barData) {
         let data = {
            Xtext: [],
            Yvlaue: []
         }

         for (let k in barData) {
            data.Xtext.push(k)
            data.Yvlaue.push(barData[k])
         }

         return data

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
      display: flex;
      width: 100%;


      .barMap {
         flex: 1;
         margin: auto;
         width: 100%;
         height: 100%;
      }

      .lineMap {
         flex: 1;
         width: 100%;
         height: 100%;
      }
   }

}
</style>