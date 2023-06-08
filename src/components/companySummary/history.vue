<!--
 描述: 发展历程
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="history-container">
    <div class="chart" id="mainChart"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "history",
  data() {
    return {

    }
  },
  mounted() {
    this.getEChart();
  },
  methods: {
    getEChart() {
      let chartDom = document.getElementById('mainChart');
      let myChart = echarts.init(chartDom, 'dark');
      let option;

      option = {
        backgroundColor: '',
        tooltip: {
          show: 'item'
        },
        legend: {
          show: false,
          top: 'bottom'
        },
        toolbox: {
          show: false,
          feature: {
            mark: { show: true },
            dataView: { show: true, readOnly: false },
            restore: { show: true },
            saveAsImage: { show: true }
          }
        },
        series: [
          {
            name: 'Nightingale Chart',
            type: 'pie',
            radius: [20, 100],
            center: ['50%', '50%'],
            roseType: 'area',
            itemStyle: {
              borderRadius: 8
            },
            data: [
              { value: 3153, name: '生活' },
              { value: 2501, name: '游戏' },
              { value: 1152, name: '影视' },
              { value: 881, name: '动画' },
              { value: 709, name: '舞蹈' },
              { value: 609, name: '运动' },
              { value: 355, name: '美食' },
              { value: 329, name: '音乐' }
            ]
          }
        ]
      };

      myChart.setOption(option, true);
      window.addEventListener('resize', () => {
        myChart.resize();
      });
    }
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style lang="scss" scoped>
.history-container {
  .chart {
    height: 3rem;
  }
}
</style>
