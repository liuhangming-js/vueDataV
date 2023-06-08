<script>
import * as echarts from 'echarts';
export default {
  data() {
    return {
      chartData: ""
    }
  },
  mounted() {
    this.chartInit();
  },
  methods: {
    chartInit() {
      let myChart = echarts.init(document.getElementById('chart_right2'), 'dark');

      console.log(1);
      const data = {};

      this.$axios.post("http://10.2.0.138:8080/api/v1/video/videotime", data, {
        headers: {
          'Content-Type': 'application/json'
        }
      }).then((res) => {
        this.chartData = res.data.data;
        this.chartData.push({
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
        });

        this.chartData = JSON.parse(this.chartData);

        console.log(this.chartData);
        console.log(2);
      });

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
            // data: [
            //   { value: 1048, name: 'Search Engine' },
            //   { value: 735, name: 'Direct' },
            //   { value: 580, name: 'Email' },
            //   { value: 484, name: 'Union Ads' },
            //   { value: 300, name: 'Video Ads' },
            //   {
            //     // make an record to fill the bottom 50%
            //     value: 1048 + 735 + 580 + 484 + 300,
            //     itemStyle: {
            //       // stop the chart from rendering this piece
            //       color: 'none',
            //       decal: {
            //         symbol: 'none'
            //       }
            //     },
            //     label: {
            //       show: false
            //     }
            //   }
            // ]
            data: this.chartData
          }
        ]
      };

      myChart.setOption(option, true);
    }
  }
}
</script>

<template>
  <div>
    {{this.chartData[5]}}
    <div id="chart_right2" style="width: 200px; height: 500px"></div>
  </div>
</template>

<style scoped lang="scss">

</style>