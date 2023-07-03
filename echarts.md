[TOC]



# 一、ECharts基本使用

**基本使用步骤**：

1.  引入echarts.js文件 【vue中使用npm 并使用 import * as echarts from 'echarts'引入】
2.  准备一个呈现图表的盒子
3.  初始化echarts实例对象
4.  ==准备配置项==。

## 1. 配置项

-  xAxis:直角坐标系中的×轴
-  yAxis:直角坐标系中的y轴
-  series:系列列表。每个系列通过type决定自己的图表类型

<a href='[Documentation - Apache ECharts](https://echarts.apache.org/zh/option.html#title)'>其他配置项</a>.

### 通用配置

#### 标题title

- 文字样式
  - textStyle

- 标题边框
  - borderWidth、borderColor 、borderRadius
- 标题位置
  - left、top、right、 bottom

#### 提示tooltip

提示框组件,用于配置鼠标滑过或点击图表时的显示框

- 触发类型: trigger
  - 可选值：item[鼠标需移到图形内部]、axis[鼠标只需要移到图形的轴上]
- 触发时机: triggerOn
  - 可选值：mouseover、click
- 格式化: formatter
  - 字符串模板，【模板变量有{a},{b}....具体见文档】
  - 回调函数，第一个参数是触发事件的对象

#### 工具按钮toolbox

ECharts提供的工具栏

显示工具栏按钮feature

内置有导出图片，数据视图，动态类型切换，数据区域缩放，重置五个工具

```js
var option={
        xAxis:{  
            type:'category',
            data:['小明','小红','小王']
        },
        yAxis:{
            type:'value',
        },
        series:[
            {
                name:'语文',
                type:'bar',
                data:[70,92,87]
            }
        ],
        toolbox:{
            feature:{//空对象即可开启功能
                saveAsImage:{},  //导出图片
                dataView:{},   //显示数据视图
                restore:{},    //重置
                dataZoom:{},   //区域缩放
                magicTyoe:{    // 图标类型切换
                    type:['图标类型名','图标类型名']
                }
            }
        },
    };
```



#### 筛选图例legend

图例,用于筛选系列,需要和series配合使用

```js
var option={
        xAxis:{  
            type:'category',
            data:['小明','小红','小王']
        },
        yAxis:{
            type:'value',
        },
        legend:{
            data:['语文','数学'] //series中数据的name
        }
        series:[
            {
                name:'语文',
                type:'bar',
                data:[70,92,87]
            },
            {
                name:'数学',
                type:'bar',
                data:[60,22,97]
            }
        ],
    };
```

### 坐标系配置

#### 网格grid

grid是用来控制直角坐标系的布局和大小

x轴和y轴就是在grid的基础上进行绘制的

```js
var option={
        grid:{
            show:true, //开启网格
            borderWidth:10, //边框宽度
            borderColor:'red',//边框颜色
            left:20, //right,top 等控制网格位置
            width:200, //height 等控制网格大小
        },
        series:[
        ],
    };
```



#### 坐标轴axis

坐标轴分为x轴和y轴

一个grid中最多有两种位置的x轴和y轴

- **坐标轴类型type**:
  - value:数值轴，自动会从目标数据中读取数据
  - category:类目轴，该类型必须通过data设置类目数据

- **显示位置**：
  - xAxis:position可取值为top或者bottom
  - yAxis:position可取值为left或者right

#### 区域缩放dataZoom

datazoom用于区域缩放，对数据范围过滤,x轴和y轴都可以拥有

datazoom是一个数组，意味着可以配置多个区域缩放器

- **类型type**:

  - slider:滑块【开启后会提供一个缩放图表的滑块】

  - inside:内置，依靠鼠标滚轮或者双指缩放

  - ```js
    var option={
            dataZoom:[
                {
                    type:'silder'
                    xAxisIndex:0 //指明作用与第0个x轴
                },
                {
                    type:'silder'
                    yAxisIndex:0 //指明作用与第0个y轴
                }
            ]
            series:[
            ],
        };
    ```
    

- **指明产生作用的轴**:
  - xAxisIndex:设置缩放组件控制的是哪个x轴，一般写0即可
  - yAxisIndex:设置缩放组件控制的是哪个y轴，一般写0即可

- **指明初始状态的缩放情况**：【也能起到一定的筛选作用】
  - start:数据窗口范围的起始百分比
  - end:数据窗口范围的结束百分比

## 2. 常用图表

### 柱状图-bar

#### 基本实现

```js
//ECharts最基本的代码结构:
//引入js文件,DOM容器,初始化对象,设置option
<script src="./echarts.min.js"></script>
<body>
    <div style="width: 600px;height: 400px;">
    </div>
</body>
<script>
    var mCharts=echarts.init(document.querySelector('div'));//初始echarts实例对象，并传递实例对象
    var option={
        xAxis:{  
            type:'category',
            data:['小明','小红','小王']
        },
        yAxis:{
            type:'value',
        },
        series:[
            {
                name:'语文',
                type:'bar',
                data:[70,92,87]
            }
        ]
    };
    //将配置项设置给echarts实例对象
    mCharts.setOption(option)
```

#### 常见效果

**标记**：

最大值、最小值：在markPoint【点标记】中配置

平均值：在markLine【线标记】中配置

```js
 series:[
            {
                name:'语文',
                type:'bar',
                markPoint:{
                    data:[
                        {
                            type:'max',name:'最大值'
                        },
                        {
                            type:'mix',name:'最小值'
                        }
                    ]
                },
                markLine:{
                    data:[
                        {
                            type:'average',name:'平均值'
                        }
                    ]
                },
                data:[70,92,87]
            }
        ]
```



**显示**：

数值显示：label

柱宽度 :barWidth

横向柱状图:更换xAxis与yAxis的属性

```js
 series:[
            {
                name:'语文',
                type:'bar',
                label:{
                    show:true,//是否显示
                    rotate:60,//旋转
                    position:'top' //文本标签位置
                },
                data:[70,92,87]
            }
        ]
    };
```



### 折线图-line

#### 基本实现

```js
//ECharts最基本的代码结构:
//引入js文件,DOM容器,初始化对象,设置option
<script src="./echarts.min.js"></script>
<body>
    <div style="width: 600px;height: 400px;">
    </div>
</body>
<script>
    var mCharts=echarts.init(document.querySelector('div'));
    var option={
        xAxis:{  
            type:'category',
            data:['一月','二月','三月','四月','五月','六月','七月']
        },
        yAxis:{
            type:'value',   
        },
        series:[
            {
                name:'语文',
                type:'line', //图标类型
                data:[3000,2000,1200,1555,800,3100,1900],
                markArea:{  //区域标注
                    data:[
                        [
                            {
                                xAxis:'一月'
                            },
                            {
                                xAxis:'二月'
                            }
                        ],
                        [
                            {
                                xAxis:'三月'
                            },
                            {
                                xAxis:'四月'
                            }
                        ]
                    ]
                }
            },   
        ]
    };
    //将配置项设置给echarts实例对象
    mCharts.setOption(option)
```



#### 常见效果

- **标记**:
  - 最大值、最小值：在markPoint【点标记】中的data配置
  - 平均值：在markLine【线标记】中的data配置
  - 标注区间：在markarea【区域标记】中的data中以数组形式表示开始值，与结束值

- **线条控制**：

  - smooth:控制是否平滑,设置值为true即可

  - lineStyle:控制线条风格

    ```js
    lineStyle:{
        color:'red',//线条颜色
        type:'solid', //线条风格 三种 dashed[虚线] dotted[点] solid
    }
    ```

- **填充风格**：
  - areaStyle:控制图标数据区域的风格

- **紧挨边缘**：
  - boundaryGap：控制折线的点【类目轴】，距离边缘的距离【例如第一个点是否在y轴上】

- **缩放**：
  - scale:true,脱离0值比例【一般用于数值轴上】

- **堆叠图**：
  - stack: 在series中给每一个需要堆叠的折线图添加stack:'all'即可
  - 堆叠的意思是，让原本各自显示的折线图，变成后一个折线图的数据累加前一个折线图的数据进行显示

### 散点图-scatter

散点图可以帮助推断出变量间的相关性

#### 基本实现

- ECharts最基本的代码结构:
  - 引入js文件,DOM容器,初始化对象,设置option
- x轴数据和y轴的数据:二维数组
  - 比如：数组1:[[身高1,体重1]，[身高2,体重2],[身高3,体重3] ...
- 图表类型︰
  - 在series下设置type:scatter
  - xAxis和yAxis的type都要设置为value

- 调整：
  - 设置scale：true,脱离0值比例



#### 常见效果

- 气泡图效果：

  - 需要：散点的大小不同

    - ```js
      series:[
          {
              ......,
           // symbolSize:80  可以单纯的只设置所有散点的大小数值
              symbolSize:function(arg){//可以是一个回调函数，参数为每一个散点的数据数组，从而通过这个数据来返回不同的数值
              return 80;
          }
          }
      ]
      ```

  - 需要：散点的颜色不同

    - ```
      series:[
          {
              ......,
              color:function(arg){ //参数为每一个散点的数据对象，其中有一个属性data数组存放散点数据，从而通过这个数据来返回不同的数值
              return 'pink' //返回值需要表示颜色的字符串
          }
          }
      ]
      ```

     

- 涟漪动画效果：

  - type:effectScatter  开启涟漪动画

  - rippleEffect:{} 用于控制涟漪动画效果

  - showEffectOn:'',控制涟漪触发时机，可选值 render【散点自动获取效果】 ，emphasis【鼠标滑过触发】

  - ```js
    series:[
        {
            ......,
            type:effectScatter,
            showEffectOn:'emphasis'
            rippleEffect:{
                scale:10 //缩放比例
        }
    ]
    ```

    

### 饼图-pie

#### 基本实现

- ECharts最基本的代码结构:
- 数据:对象数组
  - 比如：[{name:'淘宝',value:11220},{name:'京东',value:1220}] ...
- 图表类型︰
  - 在series下设置type:pie

#### 常见效果

- **显示数值**：

  - label.formatter

  - ```js
    series:[
        type:'pie',
        data:[],
        label:{  //饼图文字的显示
            show:true,  // 显示文字
            //formatter:'想显示的内容' 决定文字显示的内容
            formatter:function(arg){
                //参数arg以对象的形式包含了每块饼图的各种信息，如颜色，所占百分比等等
                return '显示的内容'
            }
        }
            
    ]
    ```

- **圆环**：

  - radius:20，   直接设置饼图的半径，
  - radius:'20%', 此时参照物为饼图所在容器宽高较小的那个的一半的长度的20%作为半径
  - radius:['50%','70%']  第0个元素代表的是内圆的半径，第一个是外圆的半径

- **男丁格尔图**：
  - roseType:'radius' 即可开启，南丁格尔图饼图的每一个区域的半径是不同的，随着数值变化改变

- **选中效果**：
  - selectedMode:'single'  选中的效果,能够将选中的区域偏离圆点一小段距离
  - selectedMode:'multiple' 效果同上，但可以选中多个
  - selectedOffset:30  修改点击过后的偏移距离

### 地图-map

**地图图表的使用方式**：

- 百度地图API
  - 需要申请百度地图ak
- 矢量地图
  - 需要准备矢量地图数据

#### 基本实现

**矢量地图实现步骤**：

- ECharts最基本的代码结构
- 准备矢量地图json文件,放到目录下
  - 或者前往<a href='http://datav.aliyun.com/tools/atlas/index.html#&lat=30.332329214580188&lng=106.72278672066881&zoom=3.5'>地图工具</a>。
- 使用Ajax获取china.json
- 在回调函数中往echarts全局对象注册地图的json数据
  - echarts.==**registerMap**==('chinaMap' , chinaJson);

- 在geo下设置【不再是配置series】
  - type:'map'
  - map:'chinaMap'

```js
     var data=[ //控制地图颜色显示数据
        {name:'北京市',value:13},
        {name:'天津市',value:55},
        {name:'上海市',value:88},
        {name:'重庆市',value:56},
        ]
    var mCharts = echarts.init(document.querySelector('div'));
    var xhr = new XMLHttpRequest();
    new Promise(reslove => {
        xhr.open('GET', 'https://geo.datav.aliyun.com/areas_v3/bound/100000_full.json')
        xhr.send();
        xhr.onreadystatechange = function (e) {
            try {
                let a = JSON.parse(xhr.responseText);
                echarts.registerMap('chinaMap', a) //向echarts全局对象中注册
                reslove(1)
            } catch {
                console.log('错误');
            }

        }

    }).then(() => {
        var option = {
            geo: {
                type: 'map',
                map: 'chinaMap' //指定地图的依赖数据，map的值需要和registerMap中的第一个参数保持一致
            },
            series:[
                {
                    data:data,
                    geoIndex:0, //配置到第几个geo，这里只有一个，因此是0
                    type:'map'  //表明是为地图进行服务
                },
                {
                  data:[{value:[118.767413, 32.041544]}], //散点的坐标数据
                    type:'effectScatter',
                    coordinateSystem:'geo',  //指明散点使用的坐标系统
                    rippleEffect:{
                        scale:5
                    }
                }
            ],
            visualMap:{
                min:0,
                max:88,
                inRange:{
                    color:['white','red']  //控制颜色渐变范围
                }
            }
        }
        mCharts.setOption(option)
    })

```



#### 常用配置

- **缩放拖动**：
  - roam:true    开启缩放拖动 在geo下配置

- **名称显示**：
  - label:{show:true}  展示标签

- **初始化缩放比例**：
  - zoom:1     初始化缩放比例
- **地图中心点**：
  - cetnter：[x坐标，y坐标]      可以通过地图矢量数据获取到的某个具体位置

#### 常见效果

- **显示某个区域**：
  - 加载该区域的矢量地图数据
  - 通过registerMap注册到echarts全局对象中
  - 指明geo配置下的type和map属性
  - 通过zoom放大该区域
  - 通过center定位中心点
- **不同城市颜色不同**：
  - 显示基本的中国地图
  - 城市的空气质量数据设置给series
  - 将series下的数据和geo关联起来
    - geoIndex:0、 type:'map'
  - 结合visualMap配合使用
    - 需指明min、max、inRange【变化范围】、calculable:true 【出现滑块】

- **地图和散点图结合**：
  - 给series下增加新的对象
  - 准备好散点数据,设置给新对象的data
  - 配置新对象的type
    - type:effectScatter
  - 让==散点图使用地图坐标系统==。
    - coordinateSystem: 'geo',
  - 让涟漪的效果更加明显



### 雷达图-radar

#### 基本实现

- ECharts最基本的代码结构:
- **定义各个维度的最大值**：
  - 如： indicator:[ { name: '易用性', max: 100},..…]
- **准备具体产品的数据**：
  - 如： data:[ {name: '华为手机1', value: [80,90,80,82,90] },..... ]
- **图表类型**︰
  - 在series下设置type:radar

```js
    var mCharts = echarts.init(document.querySelector('div'));
   //配置各个未读最大值
    var dataMax = [
        {
            name: '攻击',
            max: 100
        },
        {
            name: '防御',
            max: 100
        },
        {
            name: '速度',
            max: 100
        },
        {
            name: '智力',
            max: 100
        },
        {
            name: '生命',
            max: 100
        },
    ]
    var option = {
        radar: {
            indicator: dataMax
        },
        series: [
            {
                type:'radar',
                data: [
                    {
                        name: '战士',
                        value: [70, 85, 70, 50, 80]
                    }, {
                        name: '刺客',
                        value: [90, 50, 80, 60, 60]
                    }
                ]
            }
        ]
    };
    mCharts.setOption(option)
```

#### 常用配置

- **显示数值**：
  - label
- **区域面积**：
  - areaStyle
- **绘制类型**：
  - shape:'circle'  绘制形状为圆形  默认值为‘polygon’ 多边形

### 仪表盘图-gauge

#### 基本实现

- ECharts最基本的代码结构:
- 准备数据,设置给series下的data
  - data:[{value: 97}]
- 图表类型∶
  - 在series下设置type:gauge

#### 常见效果

- **数值范围**：
  - max、min

- **多个指针**：
  - 增加data中的数组元素
- **多个指针颜色差异**：
  - itemStyle:{color:''}

# 二、ECharts进阶

## 1. 显示相关

### 主题

- **内置主题**
  - ECharts中默认内置了两套主题:light dark
  - 在初始化对象方法init中可以指明
    var chart = echarts.init(dom, 'light');
- **自定义主题**
  - 1.在主题编辑器中编辑主题
  - 2.下载主题,是一个js文件
  - 3.引入主题js文件
  - 4.在init方法中使用主题

### 调色板

它是一组颜色，图形、系列会自动从其中选择颜色。

- **主题调色盘**：
  - 在主题文件中的echarts.registerTheme('主题名'，{"color":[]})中配置
- **全局调色盘**：
  - option:{color:['','']} 中设置 且会覆盖主题当中设置的调色盘
- **局部调色盘**：
  - series:[{color:['','']}] 调色盘的作用遵循就近原则

#### 颜色渐变

- **线性渐变**：

  - ```js
     itemStyle:{
                        color:{
                            type:'linear',  //渐变类型
                            //渐变方向 这里相当于(0,0)->(0,1) 方向向下
                            x:0, 
                            y:0,
                            x2:0,
                            y2:1,
                            colorStops:[{
                                offset:0,color:'red'  //%0处的颜色
                            },{
                                offset:1,color:'blue' //%100处的颜色
                            }],
                            globalCoord:false
                        }
                    }
    ```

- **径向渐变**：

  - ```js
    itemStyle:{
                        color:{
                            type:'radial',  //渐变类型
                            x:0.5, //圆心坐标
                            y:0.5,
                            r:1, //半径辐射范围
                            colorStops:[{
                                offset:0,color:'red'  //%0处的颜色
                            },{
                                offset:1,color:'blue' //%100处的颜色
                            }],
                            globalCoord:false
                        }
                    }
    ```
    

### 样式

- **直接样式**：
  - itemStyle【控制某一数据对象样式】、textStyle【控制标题样式】、lineStyle、areaStyle、label
- **高亮样式**：
  - 在数据对象中对象属性emphasis中包裹itemstyle、textStyle、linestyle、areaStyle、label

### 自适应的实现

当浏览器的大小发生变化的时候,如果想让图表也能随之适配变化

- 监听窗口大小变化事件
- 在事件处理函数中调用ECharts实例对象的resize即可
  - window.onresize = function(){myChart.resize();} 或者  window.onresize=myChart.resize

## 2. 动画的使用

### 加载动画

ECharts已经内置好了加载数据的动画,只需要在合适的时机显示或者隐藏即可【一般用于网络速度偏慢，图表不能快速加载时使用，通过显示加载的方式提供使用体验】

- **显示加载动画**：
  - mCharts.showLoading()
- **隐藏加载动画**：
  - mCharts.hideLoading()

### 增量动画

- **增量动画的实现方式**：
  - mCharts.setOption 。 也就是当数据发送变化时，修改数据后，再次调用setOption，且新旧option是整合而不是覆盖，因此设置新数据时，只用关注变化的数据

### 动画的配置

- **开启动画**：
  - animation:true  默认值就是开启的
- **动画时长**：
  - animationDuration:7000  控制动画所需时长，单位为毫秒
  - animationDuration: function( arg ){return}   参数arg为将能够产生动画的元素分类之后，再依次赋予的编号，每一类都由0，1，2.....开始
- **缓动动画**：
  - animationEasing:'bounceOut'  有匀速、加速、等等。
- **动画阈值**：
  - animationThreshold:8
  - 单种形式的元素数量大于这个阈值时会关闭动画

## 3. 交互API

### 全局echarts对象

全局echarts对象是引入echarts.js文件之后就可以直接使用的

```js
<script src="./echarts.min.js"></script>
var mCharts = echarts.init(document.querySelector('div'));
//echarts就是全局echarts对象
```

#### 常见方法

- **init方法**：

  - 初始化ECharts实例对象
  - 使用主题：只有注册过的主题,才能在init方法中使用该主题

- **registerTheme方法**：

  - 注册主题

- **registerMap方法**：

  - 注册地图数据，使得geo组件可以使用地图数据

- **connect方法**：

  - 一个页面中可以有多个独立的图表

  - 每一个图表对应一个ECharts实例对象

  - connect可以实现多图关联，传入联动目标为ECharts实例对象，支持数组。

    - ```js
      echarts.connect([mCharts1,mCharts2])
      ```

    - 保存图片的自动拼接【比如只在第一个图标上开启了下载图片，关联以后可同时将其他关联图标一同下载】

    - 刷新按钮

    - 重置按钮

    - 提示框联动、图例选择、数据范围修改等....

### echartsInstance对象

eChartslnstance对象是通过echarts.init方法调用之后得到的

```js
<script src="./echarts.min.js"></script>
var mCharts = echarts.init(document.querySelector('div'));
//mCharts就是echartsInstance对象
```

#### 常见方法

- **setOption方法**：

  - 设置或修改图表实例的配置项以及数据
  - 多次调用setOption方法

- **resize方法**：

  - 重新计算和绘制图表
  - 一般和window对象的resize事件结合使用 window.onresize=myCharts.resize

- **on\off方法**：

  - 绑定或者解绑事件处理函数鼠标事件
  -  mcharts.on('click',function(arg){}) 参数arg包含触发事件区域的信息
  - 鼠标常见事件: 'click'、'dblclick'、 'mousedown'、'mousemove'、'mouseup'等
  - ECharts常见事件: legendselectchanged、 'datazoom'、 'pieselectchanged'、 'mapselectchanged'等
  - 更多ECharts事件可见<a href='[Documentation - Apache ECharts](https://echarts.apache.org/zh/api.html#echarts)'>图标API</a>.

- **dispacthAction方法**：

  - 触发某些行为

  - 使用代码模拟用户的行为

  - ```js
    myCharts.dispatchAction({
        type:'highlight',//事件类型
        seriesIndex:0,//图标索引
        dataIndex:1// 图标哪一项高亮
    })
    ```

- **clear方法**：

  - 清空当前实例，会移除实例中所有的组件和图表
  - 清空之后可以再次setOption

- **dispose方法**：

  - 销毁实例