<template>
  <div ref="chart"></div>
</template>

<script>
  import {$, extend, resizeMixin} from 'assets/js/common.js'
  import {dataZoom, tooltipStyle, axisLabel} from 'assets/js/echarts-style'

  export default {
    name: 'barecharts',
    mixins: [resizeMixin],
    props: {
      chartBar: {
        type: Object,
        default: () => {
        }
      }
    },
    data() {
      return {
        myChart: null
      }
    },
    watch: {
      echartsData: {
        handler: function (val, oldVal) {
          this.initChart()
        },
        deep: true  //增加deep 观察对象的子对象变化
      }
    },
    mounted() {
      this.myChart = this.$echarts.init(this.$refs.chart);
      this.$nextTick(() => {
        this.initChart()
      })
    },

    computed: {},
    methods: {
      initChart() {
        let echartOpt = {
          fz: '16',
          color: '#fff'
        };
        if (Object.keys(this.chartBar).length) {

          let option = {
            tooltip: {
              ...tooltipStyle,
              trigger: 'axis',
            },
            calculable: true,
            grid: {
              left: '1%',
              right: '1%',
              top: '20%',
              bottom: '10%',
              containLabel: true
            },
            legend: {
              show: true,
              top: 0,
              itemWidth: 15,
              itemHeight: 7,
              top: '15',
              itemGap: 30, //两图例之间距离
              data: [{
                name: "食品类居民消费价格指数",
                textStyle: {
                  fontSize: 16,
                  color: "#fff",
                  padding: [0, 5]
                }
              }, {
                name: "国内生产总值",
                textStyle: {
                  fontSize: 16,
                  color: "#fff",
                  padding: [0, 5]
                },
              },
                {
                  name: "苹果总净出口量",
                  textStyle: {
                    fontSize: 16,
                    color: "#fff",
                    padding: [0, 5]
                  },
                },
                {
                  name: "国内苹果产量",
                  textStyle: {
                    fontSize: 16,
                    color: "#fff",
                    padding: [0, 5]
                  },
                }
              ]
            },
            xAxis: [
              {
                name: '',
                type: 'category',
                data: this.chartBar.Xdata,
                axisPointer: {
                  type: 'shadow'
                },
                axisLine: {
                  show: true,
                  lineStyle: {
                    type: 'dotted',
                    color: '#794A24'
                  }
                },
                axisTick: {
                  show: false
                },
                axisLabel: axisLabel,
              }
            ],
            yAxis: [
              {
                type: 'value',
                name: '弹性系数',
                nameTextStyle: {
                  fontSize: 16,
                  color: '#fff'
                },
                axisLine: {
                  show: false
                },
                axisTick: {
                  show: false
                },
                splitLine: {
                  show: true,
                  lineStyle: {
                    type: 'dotted',
                    color: '#114970'
                  }
                },
                axisLabel: axisLabel,
              }
            ],
            color: ["#40b0fc", "#0e62d4", "#4c58b1", "#c37837", "#c0bb3e"],
            series: [
              {
                name: '食品类居民消费价格指数',
                type: 'bar',
                barWidth: 40,
                barGap: 1,
                data: this.chartBar.data1,
                label: {
                  normal: {
                    show: true,
                    position: 'top',
                    color: '#fff',
                    fontSize: 16
                  }
                },
//              markLine: {
//                symbolSize: 7,
//                data: [
//                  {
//                    type: '',
//                    name:'-1',
//                    yAxis:-1
//                  },
//
//                ],
//                lineStyle:{
//                  normal:{
//                    color:'#FC6500'
//                  }
//                }
//              }
              },
              {
                name: '国内生产总值',
                type: 'bar',
                barWidth: 40,
                barGap: 1,
                data: this.chartBar.data2,
                label: {
                  normal: {
                    show: true,
                    position: 'top',
                    color: '#fff',
                    fontSize: 16
                  }
                },
              },
              {
                name: '苹果总净出口量',
                type: 'bar',
                barWidth: 40,
                barGap: 1,
                data: this.chartBar.data3,
                label: {
                  normal: {
                    show: true,
                    position: 'top',
                    color: '#fff',
                    fontSize: 16
                  }
                },
              },
              {
                name: '国内苹果产量',
                type: 'bar',
                barWidth: 40,
                barGap: 1,
                data: this.chartBar.data4,
                label: {
                  normal: {
                    show: true,
                    position: 'top',
                    color: '#fff',
                    fontSize: 16
                  }
                },
              }
            ]
          }
          //如果有新的配置项的变化 深度拷贝
          if (Object.keys(this.chartBar.option).length) {
            option = $.extend(true, option, this.chartBar.option)
          }
          this.myChart.setOption(option, true);
        }
      },
      // echats 图表自适应
      _windowResizeHandler() {
        this.myChart.resize()
      },
      // 销毁echats图表方法
      _destroyEchart() {
        this.myChart.dispose()
      }

    }


  }
</script>

<style lang="scss" scoped>
  @import "./../../../assets/css/_variable.scss";
  @import "./../../../assets/css/_mixin.scss";


</style>
