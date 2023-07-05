<template>
    <div class="pieImgContainer">
        <div class="pieImgView"></div>
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
        pieImgData: {
            type: Array,
            default: []
        }
    },
    data() {
        return {

        }
    },
    computed: {

    },
    watch: {

    },
    mounted() {
        this.showPieImg(this.pieImgData)
    },
    methods: {
        showPieImg(data) {
            let myCharts = echarts.init(document.querySelector('.pieImgView'));
            let option = {
                title: {
                    text: data[0].name,
                    subtext: `${data[0].value}%`,
                    left: 'center',
                    top: 'center',
                    textStyle:{
                        color:'rgb(44,246,249)'
                    },
                    subtextStyle:{
                        color:'rgb(44,246,249)'
                    },
                   
                },
                series: [
                    {
                        type: 'pie',
                        data: data,
                        label: {
                            show: true,
                            position: 'inner',
                            formatter: function (arg) {
                                return `${arg.data.name}`
                            }
                        },
                        radius: ['40%', '80%'],
                        selectedMode: 'single'
                    }
                ]
            }
            myCharts.on('mouseover', function (params) {
               const {name,value}=params.data;
               myCharts.setOption({
                    title: {
                    text: name,
                    subtext: `${value}%`,
                    left: 'center',
                    top: 'center',
                    textStyle:{
                        color:'rgb(44,246,249)'
                    },
                    subtextStyle:{
                        color:'rgb(44,246,249)'
                    },
                   
                },

            })
            })




            myCharts.setOption(option)
        }
    }
};
</script>
<style lang='scss' scoped>
.pieImgContainer {
    box-sizing: border-box;
    width: 100%;
    height: 100%;
  

    .pieImgView {
        width: 100%;
        height: 100%;
        div{
            padding: 1rem;
        }
    }
}
</style>