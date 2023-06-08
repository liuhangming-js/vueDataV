<!--
 描述: 产品热词
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="word-container">
    <div class="chart" id="chart_right1"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts';
import "echarts-wordcloud/dist/echarts-wordcloud";
import "echarts-wordcloud/dist/echarts-wordcloud.min.js";

export default {
  name: "wordCloud",
  data() {
    return {
      wordData: []
    }
  },
  mounted() {
    this.getEchartRight1();
    // this.timer = setInterval(() => {
    //   this.getEchartRight1();
    // }, 5000)
  },
  methods: {
    getEchartRight1() {
      let myChart = echarts.init(document.getElementById('chart_right1'), 'dark');

      this.$axios.post("http://10.2.0.138:8080/api/v1/video/frequency", {}, {
        headers: {
          'Content-Type': 'application/json'
        }
      }).then((res) => {
        let midData = res.data.data;
        this.wordData.push(midData[1]);
        this.wordData.push(midData[2]);
        this.wordData.push(midData[3]);
        this.wordData.push(midData[5]);
        this.wordData.push(midData[7]);
        this.wordData.push(midData[10]);
        this.wordData.push(midData[14]);
        this.wordData.push(midData[16]);
        this.wordData.push(midData[21]);
        this.wordData.push(midData[23]);
        this.wordData.push(midData[24]);
        this.wordData.push(midData[25]);
        this.wordData.push(midData[26]);
        this.wordData.push(midData[27]);
        this.wordData.push(midData[28]);
        this.wordData.push(midData[29]);
        this.wordData.push(midData[30]);
        this.wordData.push(midData[31]);
        this.wordData.push(midData[32]);
        this.wordData.push(midData[33]);

        myChart.setOption({
          backgroundColor: '',
          series: [{
            type: 'wordCloud',
            gridSize: 1,
            sizeRange: [25, 100],
            rotationRange: [-90, 90],
            rotationStep: 45,
            shape: 'diamond',
            width: '90%',
            textPadding: 0,
            autoSize: {
              enable: true,
              minSize: 6
            },
            textStyle: {
              normal: {
                color: function () {
                  return 'rgb(' + [
                    Math.round(Math.random() * 160),
                    Math.round(Math.random() * 160),
                    Math.round(Math.random() * 160)
                  ].join(',') + ')';
                }
              },
              emphasis: {
                fontSize: 20
              }
            },
            data: this.wordData
          }]
        })
      });

      window.addEventListener('resize', () => {
        myChart.resize();
      });
    },
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style lang="scss" scoped>
.word-container {
  .chart {
    height: 3rem;
  }
}
</style>
