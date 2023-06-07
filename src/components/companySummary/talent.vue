<!--
 描述: 人才队伍
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
  <div class="talent-container"> 
    <div class="chart" id="chart_left2"></div>   
  </div>
</template>

<script>
import * as echarts from 'echarts';

export default {
  name: "talent",
  data() {
    return {
      
    }
  },
  mounted() {
    this.getEchartLeft2();
  },
  methods: {
    getEchartLeft2() {
      let myChart = echarts.init(document.getElementById('chart_left2'), 'dark');

      const dataBJ = [
        [4276007, 27755, 342051, 160184, 73650, 19056, 31]
      ];
      const dataGZ = [
        [118, 50, 0, 1.383, 76, 11, 31]
      ];
      const dataSH = [
        [187, 143, 201, 1.39, 89, 53, 31]
      ];
      const lineStyle = {
        width: 1,
        opacity: 0.5
      };

      let option = {
        backgroundColor: '',
        tooltip: {
          trigger: 'item'
        },
        legend: {
          orient: 'vertical',
          x: 'left',
          y: 'center',
          data: ['video1', 'video2', 'video3'],
          itemGap: 10,
          textStyle: {
            color: '#fff',
            fontSize: 14
          },
          selectedMode: 'single'
        },
        radar: {
          indicator: [
            { name: '播放量', max: 5276007 },
            { name: '弹幕数', max: 57755 },
            { name: '点赞数', max: 642051 },
            { name: '硬币数', max: 360184 },
            { name: '收藏数', max: 113650 },
            { name: '转发数', max: 59056 }
          ],
          shape: 'circle',
          splitNumber: 5,
          axisName: {
            color: 'rgb(238, 197, 102)'
          },
          splitLine: {
            lineStyle: {
              color: [
                'rgba(238, 197, 102, 0.1)',
                'rgba(238, 197, 102, 0.2)',
                'rgba(238, 197, 102, 0.4)',
                'rgba(238, 197, 102, 0.6)',
                'rgba(238, 197, 102, 0.8)',
                'rgba(238, 197, 102, 1)'
              ].reverse()
            }
          },
          splitArea: {
            show: false
          },
          axisLine: {
            lineStyle: {
              color: 'rgba(238, 197, 102, 0.5)'
            }
          }
        },
        series: [
          {
            name: 'video1',
            type: 'radar',
            lineStyle: lineStyle,
            data: dataBJ,
            symbol: 'none',
            itemStyle: {
              color: '#F9713C'
            },
            areaStyle: {
              opacity: 0.1
            }
          },
          {
            name: 'video2',
            type: 'radar',
            lineStyle: lineStyle,
            data: dataSH,
            symbol: 'none',
            itemStyle: {
              color: '#B3E4A1'
            },
            areaStyle: {
              opacity: 0.05
            }
          },
          {
            name: 'video3',
            type: 'radar',
            lineStyle: lineStyle,
            data: dataGZ,
            symbol: 'none',
            itemStyle: {
              color: 'rgb(238, 197, 102)'
            },
            areaStyle: {
              opacity: 0.05
            }
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
.talent-container {
  .chart {
    height: 3rem;
  }
}
</style>
