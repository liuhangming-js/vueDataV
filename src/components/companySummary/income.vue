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
      chartData: "",
      cmpSeries: [
        {
          name: 'Direct',
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
          name: 'Mail Ad',
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
          name: 'Affiliate Ad',
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
          name: 'Video Ad',
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
    }
  },
  mounted() {
    this.getEchartLeft3();
  },
  methods: {
    getEchartLeft3() {
      let myChart = echarts.init(document.getElementById('chart_left3'), 'dark');

      this.$axios.post("http://10.2.0.138:8080/api/v1/video/cmp", {}, {
        headers: {
          'Content-Type': 'application/json'
        }
      }).then((res) => {
        this.chartData = res.data.data;

        for (let i = 0; i < this.chartData.length; i++) {
          this.cmpSeries[i].name = this.chartData[i].name;
          this.cmpSeries[i].data = this.chartData[i].data;
          for (let j = 0; j < this.cmpSeries[i].data.length; j++) {
            this.cmpSeries[i].data[j] = Math.round(Math.random() * 5000000 + 500000);
          }
          this.cmpSeries[i].label.show = false;
        }

        myChart.setOption(
            {
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
                data: ['巴黎真的那么乱？', '自制水路两栖钓鱼房车', '《防空模拟器》', '谢谢胆子大的朋友来喝我的奶茶！', '真的会有人按下这个按钮吗？？？', '在上司的葬礼上真情流露', '不是在玩游戏，而是在练字']
              },
              series: this.cmpSeries
            }
        );
      })

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
