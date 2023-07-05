<template>
   <div class="myMapBox">
      <div class="myMapView"></div>
   </div>
</template>
<script>
import * as echarts from 'echarts'
import anHuiMap from '@/assets/anhui.json'
export default {
   name: '',
   components: {

   },
   mixins: [],
   props: {

   },
   data() {
      return {
         addressData: [
            { name: '合肥市', value: 40, },
            { name: '芜湖市', value: 50 },
            { name: '蚌埠市', value: 60 },
            { name: '淮南市', value: 70 },
            { name: '马鞍山市', value: 80 },
            { name: '淮北市', value: 90 },
            { name: '铜陵市', value: 100 },
            { name: '安庆市', value: 40 },
            { name: '黄山市', value: 50 },
            { name: '滁州市', value: 60 },
            { name: '阜阳市', value: 70 },
            { name: '宿州市', value: 80 },
            { name: '六安市', value: 90 },
            { name: '亳州市', value: 100 },
            { name: '池州市', value: 40 },
            { name: '宣城市', value: 50 }
         ],
         tooltipIndex: 0,// 新增属性
         highlightIndex: 0 // 高亮区域索引
      }
   },
   computed: {

   },
   watch: {

   },

   mounted() {
      this.showMymap()
   },
   methods: {
      showMymap() {
         echarts.registerMap('ah', anHuiMap)
         let mCharts = echarts.init(document.querySelector('.myMapView'))
         let option = {
            geo: {
               type: 'map',
               map: 'ah', //指定地图的依赖数据，map的值需要和registerMap中的第一个参数保持一致
               roam: true,
               label: {
                  show: true
               },
               top: 5,
               bottom: 10,
               left: 10,
               right: 10,
               itemStyle: {   //这里设置了最外层边框
                  normal: {
                     borderColor: 'rgb(75,146,181)',
                     areaColor: 'rgb(4,25,78)', // 设置默认区域颜色
                     shadowColor: 'rgba(255, 255, 255, 0.5)', // 设置阴影颜色为黑色
                     shadowBlur: 10, // 设置阴影模糊度为10  
                     borderWidth: 2
                  },
                  emphasis: {
                     areaColor: '#FFCC00', // 设置鼠标悬停区域颜色

                  }
               },
            },
            tooltip: {
               trigger: 'item',
               formatter: function (data) {
                  return '接入医院数' + ': ' + data.value + '<br/>';
               },
               show: true, // 显示tooltip
               transitionDuration: 0, // 去除tooltip的渐变效果
     
               // 自动轮播
               // triggerOn: 'none', // 手动触发tooltip
               extraCssText: 'user-select: none;', // 禁止手动选择tooltip内容
               enterable: true, // 鼠标可进入tooltip
               confine: true, // tooltip限制在图表区域内

               // 鼠标进入区域时触发的事件
               onmouseover: (params) => {
                  this.tooltipIndex = params.dataIndex; // 记录当前显示的索引
                  this.highlightIndex = params.dataIndex; // 高亮当前区域
                  mCharts.dispatchAction({
                     type: 'highlight',
                     dataIndex: this.highlightIndex
                  });
               },
               // 鼠标离开区域时触发的事件
               onmouseout: (params) => {
                  this.tooltipIndex = 0; // 鼠标离开后将索引重置为0
                  this.highlightIndex = 0; // 取消高亮
                  mCharts.dispatchAction({
                     type: 'downplay',
                     dataIndex: params.dataIndex
                  });
               }
            },
            series: [
               {
                  name: '地图',
                  type: 'map',
                  map: 'ah',
                  top: 5,
                  bottom: 10,
                  left: 10,
                  right: 10,
                  label: {
                     show: true,
                     color: 'white'
                  },
                  itemStyle: {
                     normal: {
                        borderColor: 'rgb(75,146,181)',
                        areaColor: 'rgb(4,25,78)', // 设置默认区域颜色
                        // shadowColor: 'rgba(255, 255, 255, 0.5)', // 设置阴影颜色为黑色
                        // shadowBlur: 10 // 设置阴影模糊度为10  

                     },
                     emphasis: {
                        areaColor: '#FFCC00', // 设置鼠标悬停区域颜色

                     }
                  },
                  data: this.addressData,


               }
            ]



         }
         mCharts.setOption(option)
         this.tooltipPlay(mCharts);
      },

         tooltipPlay(mCharts){
            setInterval(() => {
            this.tooltipIndex = (this.tooltipIndex + 1) % this.addressData.length;
            this.highlightIndex = this.tooltipIndex; // 高亮当前区域
            mCharts.dispatchAction({
               type: 'showTip',
               seriesIndex: 0,
               dataIndex: this.tooltipIndex
            });

            mCharts.dispatchAction({
               type: 'highlight',
               seriesIndex: 0,
               dataIndex: this.tooltipIndex
            });

            setTimeout(() => {
               mCharts.dispatchAction({
                  type: 'downplay',
                  seriesIndex: 0,
                  dataIndex: this.highlightIndex
               });
            }, 2800);
         }, 3000);
         }
   }
};
</script>
<style lang='scss' scoped>
.myMapBox {
   width: 100%;
   height: 100%;
   background-color: rgb(12, 16, 45);
   overflow: hidden;

   .myMapView {
      width: 100%;
      height: 100%;
   }
}
</style>