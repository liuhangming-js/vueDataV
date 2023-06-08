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

      this.$axios.post("http://10.2.0.138:8080/api/v1/video/cmp", data, {
        headers: {
          'Content-Type': 'application/json'
        }
      })
      // this.$axios.get("http://localhost:8081/data/distribution.json")
      .then((res) => {
        this.chartData = res.data.data;
        // let sum = 0;
        // for (let i = 0; i < this.chartData.length; i++) {
        //   sum += this.chartData[i].value;
        // }
        for (let i = 0; i < this.chartData.length; i++) {
          console.log(this.chartData[i].name);
          console.log(this.chartData[i].data);
        }

      });
    }
  }
}
</script>

<template>
  <div>
    {{this.chartData[0]}}
    <div id="chart_right2" style="width: 200px; height: 500px"></div>
  </div>
</template>

<style scoped lang="scss">

</style>