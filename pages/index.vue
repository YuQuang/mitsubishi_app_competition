<template>
  <div class="p-5 flex flex-wrap flex-col gap-3">
    <!-- 操作人員顯示列 -->
    <div class="flex flex-wrap justify-between">
      <div class="text-2xl font-bold">Dashboard</div>
      <div class="text-lg">Operator : Wilson.Li</div>
    </div>

    <UAlert
      icon="i-heroicons-cog-8-tooth"
      :color="machine_alert.color"
      variant="solid"
      :title="machine_alert.title"
      :description="machine_alert.description"
    />

    <!-- 數值顯示列 -->
    <div class="grid md:grid-cols-4 sm:grid-cols-2 grid-cols-1 gap-3">
      <!-- 車刀溫度 -->
      <div class="p-5 bg-slate-800/70 shadow-md shadow-slate-600/50 rounded-md">
        車刀(°C)
        <UProgress :value="chedau.temp" :max="100" :color="chedau.bar_color">
          <template #indicator>
            <div class="text-right">
              <span v-if="chedau.temp < 25" class="text-blue-500">{{ chedau.temp }}°C</span>
              <span v-else-if="chedau.temp < 50" class="text-amber-500">{{ chedau.temp }}°C</span>
              <span v-else-if="chedau.temp < 75" class="text-orange-500">{{ chedau.temp }}°C</span>
              <span v-else class="text-red-500">🔥{{ chedau.temp }}°C</span>
            </div>
          </template>
        </UProgress>
      </div>
      <!-- 铣刀溫度 -->
      <div class="p-5 bg-slate-700/80 shadow-md shadow-slate-600/50 rounded-md">
        铣刀(°C)
        <UProgress :value="xidau.temp" :max="100" :color="xidau.bar_color">
          <template #indicator>
            <div class="text-right">
              <span v-if="xidau.temp < 25" class="text-blue-500">{{ xidau.temp }}°C</span>
              <span v-else-if="xidau.temp < 50" class="text-amber-500">{{ xidau.temp }}°C</span>
              <span v-else-if="xidau.temp < 75" class="text-orange-500">{{ xidau.temp }}°C</span>
              <span v-else class="text-red-500">🔥{{ chedau.temp }}°C</span>
            </div>
          </template>
        </UProgress>
      </div>
      <!-- 夾頭速度 -->
      <div class="p-5 bg-slate-800/70 shadow-md shadow-slate-600/50 rounded-md">
        夾頭(RMP)
        <UProgress :value="jiatou.rmp" :max="10000" :color="jiatou.bar_color">
          <template #indicator>
            <div class="text-right text-red-500">{{ jiatou.rmp }}</div>
          </template>
        </UProgress>
      </div>
      <!-- 工程進度 -->
      <div class="p-5 bg-slate-700/80 shadow-md shadow-slate-600/50 rounded-md">
        工程進度(件數)
        <UProgress :value="jindu.now" :max="jindu.total" :color="jindu.bar_color">
          <template #indicator>
            <div class="text-right text-green-500">{{ jindu.now }}/{{ jindu.total }}</div>
          </template>
        </UProgress>
      </div>
    </div>

    <div class="grid grid-cols-3 gap-3">
      <!-- 座標 -->
      <div class="col-span-1 p-5 bg-slate-800/70 shadow-slate-600/50 rounded-md">
        <div class="flex flex-wrap flex-col gap-3 text-4xl">
          <div class="flex justify-between">
            <div>X</div>
            <div>{{ coordinate.x }}</div>
          </div>
          <div class="flex justify-between">
            <div>Y</div>
            <div>{{ coordinate.y }}</div>
          </div>
          <div class="flex justify-between">
            <div>Z</div>
            <div>{{ coordinate.z }}</div>
          </div>
          <div class="flex justify-between">
            <div>A</div>
            <div>{{ coordinate.a }}</div>
          </div>
          <div class="flex justify-between">
            <div>B</div>
            <div>{{ coordinate.b }}</div>
          </div>
          <div class="flex justify-between">
            <div>C</div>
            <div>{{ coordinate.c }}</div>
          </div>
        </div>
      </div>
      
      <!-- 3D範例圖 -->
      <div class="col-span-2">
        <canvas id="canvas3d" class="rounded-md"></canvas>
      </div>
    </div>

    <!-- 機台詳細情況 -->
    <div class="grid grid-cols-3 gap-3">
      <!-- 機台選擇清單 -->
      <UTable class="col-auto bg-slate-700/80 rounded-md shadow-md shadow-slate-600/50" :columns="columns" :rows="machine" />

      <!-- 機台詳細資訊 -->
      <div class="p-5 col-span-2 bg-slate-700/80 rounded-md shadow-md shadow-slate-600/50">
        <!-- 機台情況 -->
        <div class="grid grid-cols-2 text-2xl gap-3">
          <div class="col-span-2">程式編號 : {{ "061d8fcd942c".toUpperCase() }}</div>
          <div class="col-span-2">訂單名稱 : {{ "OrderName" }}</div>
          <div>材料 : {{ "木工" }}</div>
          <div>加工規格 : {{ "米字T6" }}</div>
          <div class="col-span-2">
            開始時間 : {{ program.start_time }}
          </div>
          <div>
            經過時間 : {{ program.time_elapsed }} min
          </div>
          <div>
            剩餘時間 : {{ program.time_remain }} min
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'default',
  name: 'IndexPage',
})

const columns = [{
  key: 'id',
  label: 'ID',
  sortable: true
}, {
  key: 'name',
  label: 'Name',
  sortable: true
}]

const machine = [{
  id: 1,
  name: '走道1_機器1'
}, {
  id: 2,
  name: '走道1_機器2'
}]
</script>

<script lang="ts">
import { Application } from '@splinetool/runtime';

export default {
  data(){
    return {
      chedau: {
        temp: 0,
        bar_color: 'amber'
      },
      xidau:{
        temp: 0,
        bar_color: 'amber'
      },
      jiatou: {
        rmp: 6000,
        bar_color: 'red'
      },
      jindu: {
        now: 0,
        total: 10000,
        bar_color: 'green'
      },
      coordinate: {
        x: 12,
        y: 96,
        z: 34,
        a: 40,
        b: 200,
        c: 315,
      },
      program: {
        serial: "",
        name: "",
        material: "",
        start_time: new Date(Date.now()).toISOString(),
        time_elapsed: 0,
        time_remain: 1.6,
      },
      machine_alert: {
        color: "green",
        title: "Machine is running!",
        description: "Everything is good, you can go to static page for more info."
      }
    }
  },
  mounted(){
    // Spline
    const canvas = document.getElementById('canvas3d');
    const app = new Application(canvas);
    app.load('https://prod.spline.design/JjQfYtgfvdHVF1fc/scene.splinecode');

    // Random data
    setInterval(()=>{
      this.chedau.temp = Math.floor(Math.random()*15)+30;
      this.xidau.temp = Math.floor(Math.random()*15)+30;
      this.jiatou.rmp = Math.floor(Math.random()*300)+5700;
      this.jindu.now += 100;
      if(this.jindu.now >= this.jindu.total) this.jindu.now = 0;

      this.coordinate.x = Math.floor((Math.random()*30+12)  * 1000) / 1000;
      this.coordinate.y = Math.floor((Math.random()*30+96)  * 1000) / 1000;
      this.coordinate.z = Math.floor((Math.random()*30+34)  * 1000) / 1000;
      this.coordinate.a = Math.floor((Math.random()*30+40)  * 1000) / 1000;
      this.coordinate.b = Math.floor((Math.random()*30+170) * 1000) / 1000;
      this.coordinate.c = Math.floor((Math.random()*30+315) * 1000) / 1000;

      this.program.time_elapsed += 0.016;
      this.program.time_remain -= 0.016;
      this.program.time_elapsed = Math.floor(this.program.time_elapsed*1000) / 1000;
      this.program.time_remain = Math.floor(this.program.time_remain*1000) / 1000;
      if(this.program.time_remain <= 0) this.program.time_remain = 1.6;
    }, 1000);
  },
}
</script>
