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
      chartData: ""
    }
  },
  mounted() {
    this.getEchartRight2();
  },
  methods: {
    getEchartRight2() {
      let myChart = echarts.init(document.getElementById('chart_right2'), 'dark');

      console.log(1);
      const data = {};

      this.$axios.post("http://10.2.0.138:8080/api/v1/video/videotime", data, {
        headers: {
          'Content-Type': 'application/json'
        }
      })
          // this.$axios.get("http://localhost:8081/data/distribution.json")
          .then((res) => {
            this.chartData = res.data.data;
            let sum = 0;
            for (let i = 0; i < this.chartData.length; i++) {
              sum += this.chartData[i].value;
            }
            this.chartData.push({
              // make an record to fill the bottom 50%
              value: sum,
              itemStyle: {
                // stop the chart from rendering this piece
                color: "none",
                decal: {
                  symbol: "none"
                }
              },
              label: {
                show: false
              }
            });
            console.log(this.chartData[0].value);
            console.log(this.chartData[0].name);

            myChart.setOption({
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
                  data: this.chartData
                  // data: [
                  //   {
                  //     value: 100,
                  //     name: "长视频"
                  //   },
                  //   {
                  //     value: 100,
                  //     name: "长视频"
                  //   },
                  //   {
                  //     value: 100,
                  //     name: "长视频"
                  //   },
                  //   {
                  //     value: 300,
                  //     itemStyle: {
                  //       color: "none",
                  //       decal: {
                  //         symbol: "none"
                  //       }
                  //     },
                  //     label: {
                  //       show: false
                  //     }
                  //   }
                  // ]

                }
              ]
            });
            window.addEventListener('resize', () => {
              myChart.resize()
            })
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
