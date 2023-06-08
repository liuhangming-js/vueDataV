<!--
 描述: 业务范围
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="business-container">
    <div class="chart" id="chart_left1"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "business",
  data() {
    return {

    }
  },
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      let myChart = echarts.init(document.getElementById('chart_left1'), 'dark');

      var data = [];
      for (let i = 0; i < 5; ++i) {
        data.push(Math.round(Math.random() * 200));
      }

      let option = {
        backgroundColor: "",
        xAxis: {
          max: 'dataMax'
        },
        yAxis: {
          type: 'category',
          data: ['游戏', '动画', '影视', '生活', '舞蹈'],
          inverse: true,
          animationDuration: 300,
          animationDurationUpdate: 300,
          max: 2 // only the largest 3 bars will be displayed
        },
        series: [
          {
            realtimeSort: true,
            name: 'X',
            type: 'bar',
            data: data,
            label: {
              show: true,
              position: 'right',
              valueAnimation: true
            }
          }
        ],
        legend: {
          show: false
        },
        animationDuration: 3000,
        animationDurationUpdate: 3000,
        animationEasing: 'linear',
        animationEasingUpdate: 'linear'
      };

      function update() {
        var data = option.series[0].data;
        for (var i = 0; i < data.length; ++i) {
          if (Math.random() > 0.9) {
            data[i] += Math.round(Math.random() * 200000);
          } else {
            data[i] += Math.round(Math.random() * 20000);
          }
        }
        myChart.setOption(option);
      }

      setInterval(function() {
        update();
      }, 10000);
    },
  },
  getFlag(countryName) {
    if (!countryName) {
      return '';
    }
    return (
        this.flags.find(function (item) {
          return item.name === countryName;
        }) || {}
    ).emoji;
  },

  updateYear(year) {
    let source = this.data.slice(1).filter(function (d) {
      return d[4] === year;
    });
    this.option.series[0].data = source;
    this.option.graphic.elements[0].style.text = year;
    this.chart.setOption(this.option);
  },
  beforeDestroy() {

  }
};
</script>

<style lang="scss" scoped>
.business-container {
  .chart {
    height: 3rem;
  }
}
</style>
