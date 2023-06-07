<!--
 描述: 营业收入
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="income-container"> 
    <div class="chart" id="chart_left3"></div>  
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "income",
  data() {
    return {
      
    }
  },
  mounted() {
    this.getEchartLeft3();
  },
  methods: {
    getEchartLeft3() {
      let myChart = echarts.init(document.getElementById('chart_left3'), 'dark');

      let option = {
        backgroundColor: '',
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            // Use axis to trigger tooltip
            type: 'shadow' // 'shadow' as default; can also be 'line' or 'shadow'
          }
        },
        legend: {},
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value'
        },
        yAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', '不是在玩游戏，而是在练字']
        },
        series: [
          {
            name: '点赞数',
            type: 'bar',
            stack: 'total',
            label: {
              show: true
            },
            emphasis: {
              focus: 'series'
            },
            data: [320, 302, 301, 334, 390, 330, 320]
          },
          {
            name: '投币数',
            type: 'bar',
            stack: 'total',
            label: {
              show: true
            },
            emphasis: {
              focus: 'series'
            },
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: '收藏数',
            type: 'bar',
            stack: 'total',
            label: {
              show: true
            },
            emphasis: {
              focus: 'series'
            },
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: '转发数',
            type: 'bar',
            stack: 'total',
            label: {
              show: true
            },
            emphasis: {
              focus: 'series'
            },
            data: [150, 212, 201, 154, 190, 330, 410]
          }
        ]
      };

      myChart.setOption(option, true);
      window.addEventListener('resize', () => {
        myChart.resize();
      })
    },
  },
  beforeDestroy() {
    
  }
};
</script>

<style lang="scss" scoped>
.income-container {
  .chart {
    height: 3rem;
  }
}
</style>
