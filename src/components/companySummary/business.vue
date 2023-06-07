<!--
 描述: 业务范围
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="business-container">
    {{this.res0}}
    <div class="chart" id="chart_left1"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "business",
  data() {
    return {
      ROOT_PATH: 'https://echarts.apache.org/examples',
      updateFrequency: 2000,
      dimension: 0,
      countryColors: {
        Australia: '#00008b',
        Canada: '#f00',
        China: '#ffde00',
        Cuba: '#002a8f',
        Finland: '#003580',
        France: '#ed2939',
        Germany: '#000',
        Iceland: '#003897',
        India: '#f93',
        Japan: '#bc002d',
        'North Korea': '#024fa2',
        'South Korea': '#000',
        'New Zealand': '#00247d',
        Norway: '#ef2b2d',
        Poland: '#dc143c',
        Russia: '#d52b1e',
        Turkey: '#e30a17',
        'United Kingdom': '#00247d',
        'United States': '#b22234'
      },
      chart: null,
      option: null,
      years: [],
      flags: null,
      data: null,
    }
  },
  async mounted() {
    await this.fetchData();
    this.initChart();
  },
  methods: {
    initChart() {
      const chartDom = document.getElementById('main');
      this.chart = echarts.init(chartDom);

      let startIndex = 10;
      let startYear = this.years[startIndex];
      this.option = {
        grid: {
          top: 10,
          bottom: 30,
          left: 150,
          right: 80
        },
        xAxis: {
          max: 'dataMax',
          axisLabel: {
            formatter: function (n) {
              return Math.round(n) + '';
            }
          }
        },
        dataset: {
          source: this.data.slice(1).filter(function (d) {
            return d[4] === startYear;
          })
        },
        yAxis: {
          type: 'category',
          inverse: true,
          max: 10,
          axisLabel: {
            show: true,
            fontSize: 14,
            formatter: function (value) {
              return value + '{flag|' + this.getFlag(value) + '}';
            },
            rich: {
              flag: {
                fontSize: 25,
                padding: 5
              }
            }
          },
          animationDuration: 300,
          animationDurationUpdate: 300
        },
        series: [
          {
            realtimeSort: true,
            seriesLayoutBy: 'column',
            type: 'bar',
            itemStyle: {
              color: function (param) {
                return this.countryColors[param.value[3]] || '#5470c6';
              }
            },
            encode: {
              x: this.dimension,
              y: 3
            },
            label: {
              show: true,
              precision: 1,
              position: 'right',
              valueAnimation: true,
              fontFamily: 'monospace'
            }
          }
        ],
        // Disable init animation.
        animationDuration: 0,
        animationDurationUpdate: this.updateFrequency,
        animationEasing: 'linear',
        animationEasingUpdate: 'linear',
        graphic: {
          elements: [
            {
              type: 'text',
              right: 160,
              bottom: 60,
              style: {
                text: startYear,
                font: 'bolder 80px monospace',
                fill: 'rgba(100, 100, 100, 0.25)'
              },
              z: 100
            }
          ]
        }
      };
      this.chart.setOption(this.option);

      for (let i = startIndex; i < this.years.length - 1; ++i) {
        setTimeout(() => {
          this.updateYear(this.years[i + 1]);
        }, (i - startIndex) * this.updateFrequency);
      }
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
