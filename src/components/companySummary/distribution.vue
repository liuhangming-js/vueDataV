<!--
 描述: 客户分布
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="distribution-container"> 
    <div class="chart" id="chart_right2"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "distribution",
  data() {
    return {
      
    }
  },
  mounted() {
    this.getEchartRight2();
  },
  methods: {
    getEchartRight2() {
      let myChart = echarts.init(document.getElementById('chart_right2'), 'dark');
      let option = {
        backgroundColor: '',
        tooltip: {
          trigger: 'item'
        },
        legend: {
          show: false
        },
        series: [
          {
            name: 'Access From',
            type: 'pie',
            radius: ['40%', '70%'],
            center: ['50%', '70%'],
            // adjust the start angle
            startAngle: 180,
            label: {
              show: true,
              formatter(param) {
                // correct the percentage
                return param.name + ' (' + param.percent * 2 + '%)';
              }
            },
            data: [
              { value: 75, name: '长视频' },
              { value: 117, name: '较长视频' },
              { value: 155, name: '中长度视频' },
              { value: 344, name: '较短视频' },
              { value: 27, name: '短视频' },
              {
                // make an record to fill the bottom 50%
                value: 75 + 117 + 155 + 344 + 27,
                itemStyle: {
                  // stop the chart from rendering this piece
                  color: 'none',
                  decal: {
                    symbol: 'none'
                  }
                },
                label: {
                  show: false
                }
              }
            ]
          }
        ]
      };

      myChart.setOption(option, true);
      window.addEventListener('resize', () => {
        myChart.resize();
      });
    },
  },
  beforeDestroy() {
    
  }
};
</script>

<style lang="scss" scoped>
.distribution-container {
  .chart {
    height: 3rem;
  }
}
</style>
