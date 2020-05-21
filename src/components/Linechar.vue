<template>
<div>
  <div :id="id" :class="className" :style="{height:height,width:width}" />
</div>
  <!-- echars插件 -->
</template>

<script>
import echarts from 'echarts'
import resize from '../views/Permissions/Charts/mixins/resize'

export default {
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    id: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default:'100%'
    },
    height: {
      type: String,
      default: '50vh'
    }
  },
  data() {
    return {
      chart: null,
       data: [
         "2020-04-17",
        "2020-04-18",
        "2020-04-19",
       "2020-04-20",
       "2020-04-21",
       "2020-04-22"
    
    ],
   

    }
  },
  mounted() {
    this.initChart()
    
    
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(document.getElementById(this.id))

      this.chart.setOption({
        backgroundColor: '#EAEDF1',
        title: {
          top: 20,
          text: '订单折线图',
          textStyle: {
            fontWeight: '600',
            fontSize: 16,
            color: '#292929'
          },
          left: '1%'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            lineStyle: {
              color: '#57617B'
            }
          }
        },
        legend: {
          top: 20,
          icon: 'rect',
          itemWidth: 14,
          itemHeight: 5,
          itemGap: 13,
          data: ['今日新增', '头条', '广点通','oppo','其他'],//折线图上面的小线段点击可隐藏该项
          right: '44%',
          textStyle: {
            fontSize: 12,
            color: '#292929'
          },
        },
        grid: {
          top: 100,
          left: '2%',
          right: '2%',
          bottom: '2%',
          containLabel: true
        },
        xAxis: [{
          type: 'category',
          boundaryGap: false,
          axisLine: {
            lineStyle: {
                //X轴字体颜色
              color: '#57617B'
            }
          },
          data:this.data
        }],
        yAxis: [{
          type: 'value',
          name: '',
          axisTick: {
            show: false
          },
          axisLine: {
            lineStyle: {
              color: '#57617B'
            }
          },
          axisLabel: {
            margin: 10,
            textStyle: {
              fontSize: 14
            }
          },

          //X轴线段颜色
          splitLine: {
            lineStyle: {
              color: '#CBCBCB'
            }
          }
        }],
        series: [{
          name: '今日新增',
          type: 'line',
          smooth: true,
          symbol: 'circle',
          symbolSize: 5,
          showSymbol: false,
          lineStyle: {
            normal: {
              width: 1
            }
          },
        //   areaStyle: {
        //     normal: {
        //       color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
        //         offset: 0,
        //         color: 'rgba(137, 189, 27, 0.3)'
        //       }, {
        //         offset: 0.8,
        //         color: 'rgba(137, 189, 27, 0)'
        //       }], false),
        //       shadowColor: 'rgba(0, 0, 0, 0.1)',
        //       shadowBlur: 10
        //     }
        //   },
          itemStyle: {
            normal: {
              color: 'rgb(137,189,27)',
              borderColor: 'rgba(137,189,2,0.27)',
              borderWidth: 12

            }
          },
          data: [220, 182, 191, 134, 150, 120, 110, 125, 145, 122, 165, 122] //这里是数据
        }, {
          name: '头条',
          type: 'line',
          smooth: true,
          symbol: 'circle',
          symbolSize: 5,
          showSymbol: false,
          lineStyle: {
            normal: {
              width: 1
            }
          },
        //   折线图折线背景
        //   areaStyle: {
        //     normal: {
        //       color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
        //         offset: 0,
        //         color: 'rgba(0, 136, 212, 0.3)'
        //       }, {
        //         offset: 0.8,
        //         color: 'rgba(0, 136, 212, 0)'
        //       }], false),
        //       shadowColor: 'rgba(0, 0, 0, 0.1)',
        //       shadowBlur: 10
        //     }
        //   },
          itemStyle: {
            normal: {
              color: 'rgb(0,136,212)',
              borderColor: 'rgba(0,136,212,0.2)',
              borderWidth: 12

            }
          },
          data: [120, 110, 125, 145, 122, 165, 122, 220, 182, 191, 134, 150]
        }, {
          name: '广点通',
          type: 'line',
          smooth: true,
          symbol: 'circle',
          symbolSize: 5,
          showSymbol: true,
          lineStyle: {
            normal: {
              width: 1
            }
          },
        //   areaStyle: {
        //     normal: {
        //       color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
        //         offset: 0,
        //         color: 'rgba(219, 50, 51, 0.3)'
        //       }, {
        //         offset: 0.8,
        //         color: 'rgba(219, 50, 51, 0)'
        //       }], false),
        //       shadowColor: 'rgba(0, 0, 0, 0.1)',
        //       shadowBlur: 10
        //     }
        //   },
          itemStyle: {
            normal: {
              color: 'rgb(219,50,51)',
              borderColor: 'rgba(219,50,51,0.2)',
              borderWidth: 12
            }
          },
          data: [220, 182, 125, 145, 122, 191, 134, 150, 120, 110, 165, 122]
        },
         {
          name: 'oppo',
          type: 'line',
          smooth: true,
          symbol: 'circle',
          symbolSize: 5,
          showSymbol: false,
          lineStyle: {
            normal: {
              width: 1
            }
          },
        //   areaStyle: {
        //     normal: {
        //       color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
        //         offset: 0,
        //         color: 'rgba(0, 136, 212, 0.3)'
        //       }, {
        //         offset: 0.8,
        //         color: 'rgba(0, 136, 212, 0)'
        //       }], false),
        //       shadowColor: 'rgba(0, 0, 0, 0.1)',
        //       shadowBlur: 10
        //     }
        //   },
          itemStyle: {
            normal: {
              color: 'rgb(0,136,212)',
              borderColor: 'rgba(0,136,212,0.2)',
              borderWidth: 12

            }
          },
          data: [120, 115, 135, 45, 22, 165, 122, 220, 182, 191, 134, 150]
        }, {
          name: '其他',
          type: 'line',
          smooth: true,
          symbol: 'circle',
          symbolSize: 5,
          showSymbol: false,
          lineStyle: {
            normal: {
              width: 1
            }
          },
        //   areaStyle: {
        //     normal: {
        //       color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
        //         offset: 0,
        //         color: 'rgba(255,252,0, 0.3)'
        //       }, {
        //         offset: 0.8,
        //         color: 'rgba(255,252,0, 0)'
        //       }], false),
        //       shadowColor: 'rgba(0, 0, 0, 0.1)',
        //       shadowBlur: 10
        //     }
        //   },
          itemStyle: {
            normal: {
              color: 'rgb(255,252,0)',
              borderColor: 'rgba(255,252,00.2)',
              borderWidth: 12

            }
          },
          data: [55, 120, 125, 75, 52, 65, 120, 220, 122, 51, 74, 150]
        }]
      })
    }
  }
}
</script>

<style lang="less" scoped>


</style>