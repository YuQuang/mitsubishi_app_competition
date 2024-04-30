<template>
  <div class="p-5 flex flex-wrap flex-col gap-3">
    <!-- 操作人員顯示列 -->
    <div class="flex flex-wrap justify-between">
      <div class="text-2xl font-bold">Statics</div>
      <div class="text-lg">Operator : Wilson.Li</div>
    </div>

    <div class="p-5 bg-slate-400 rounded-md text-black">
      <div class="text-md text-bold">產量分析表</div>
      <div id="produce_chart"></div>
    </div>

    <div class="p-5 bg-slate-400 rounded-md text-black">
      <div class="text-md text-bold">機台停機次數</div>
      <div id="machine_stop_chart"></div>
    </div>

    <div class="p-5 bg-slate-400 rounded-md text-black">
      <div class="text-md text-bold">機台更換零件次數</div>
      <div id="machine_repair_chart"></div>
    </div>
  </div>
</template>

<script setup lang="ts">

</script>

<script lang="ts">
import ApexCharts from 'apexcharts';

export default {
  data(){
    return {
      produce_chart_options: {
        chart: {
          height: 200,
          type: "area"
        },
        series: [
          {
            name: "走道1 機台1",
            data: [45, 52, 38, 45, 19, 23, 2]
          },
          {
            name: "走道1 機台2",
            data: [30, 60, 3, 45, 34, 77, 65]
          }
        ],
        xaxis: {
          categories: ["01 Jan", "02 Jan", "03 Jan", "04 Jan", "05 Jan", "06 Jan", "07 Jan"]
        }
      },
      machine_stop_chart_options: {
        chart: {
          height: 200,
          type: "area"
        },
        series: [
          {
            name: "走道1 機台1",
            data: [0, 1, 2, 1, 1, 0, 1]
          },
          {
            name: "走道1 機台2",
            data: [2, 0, 0, 0, 3, 0, 0]
          }
        ],
        xaxis: {
          categories: ["01 Jan", "02 Jan", "03 Jan", "04 Jan", "05 Jan", "06 Jan", "07 Jan"]
        }
      },
      machine_repair_chart_options: {
        chart: {
          height: 200,
          type: "area"
        },
        series: [
          {
            name: "走道1 機台1",
            data: [3, 2, 0, 0, 0, 0, 1]
          },
          {
            name: "走道1 機台2",
            data: [0, 0, 0, 0, 1, 0, 0]
          }
        ],
        xaxis: {
          categories: ["01 Jan", "02 Jan", "03 Jan", "04 Jan", "05 Jan", "06 Jan", "07 Jan"]
        }
      },
    }
  },
  mounted(){
    if (process.client) {
      var el = document.querySelector("#produce_chart");
      if(el) el.textContent = "";
      new ApexCharts(document.querySelector("#produce_chart"), this.produce_chart_options).render();
      
      var el = document.querySelector("#machine_stop_chart");
      if(el) el.textContent = "";
      new ApexCharts(document.querySelector("#machine_stop_chart"), this.machine_stop_chart_options).render();

      var el = document.querySelector("#machine_repair_chart");
      if(el) el.textContent = "";
      new ApexCharts(document.querySelector("#machine_repair_chart"), this.machine_repair_chart_options).render();
    }
  }
}
</script>