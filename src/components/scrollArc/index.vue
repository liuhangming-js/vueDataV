<!--
 描述: 滚动弧形线
 作者: Jack Chen
 日期: 2020-04-20
-->

<template>
  <div class="wrap-container sn-container"> 
    <div class="sn-content"> 
      <div class="sn-title">ECharts 入门示例</div>
      <div class="sn-body"> 
        <div class="wrap-container"> 
          <div class="chartsdom" id="chart_arc"></div>
        </div> 
      </div> 
    </div>   
  </div>
</template>

<script>
export default {
  name: "scrollArc",
  mounted() {
    this.getEchart();
  },
  methods: {
    getEchart() {
      let myChart = this.$echarts.init(document.getElementById('chart_arc'));
      // let myChart = echarts.init(document.getElementById('chart_arc'));
      // 指定图表的配置项和数据
      let option = {
        tooltip: {},
        legend: {
          data:['销量']
        },
        xAxis: {
          data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: [10, 20, 36, 10, 10, 20]
        }]
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);

      window.addEventListener('resize', () => {
        myChart.resize();
      });

      this.timer = setInterval(() => {
        myChart.dispatchAction({
          type: 'showTip',
          seriesIndex: 0,
          dataIndex: this.number
        });

        this.number++;

        if (this.number > this.data.length) {
          this.number = 0;
        }
      }, 1000);
    }
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style lang="scss" scoped>
.sn-container {
  left: 50px;
  top: 690px;
  width: 895px;
  height: 400px;
  .chartsdom {
    width: 100%;
    height: 95%;
  }
}
</style>
