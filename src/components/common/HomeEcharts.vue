<template>
  <div ref="pieChart" id="main" style="width: 100%; height: 500px"></div>
</template>
<script setup lang="ts">
import { onMounted, ref } from "vue";
import * as echarts from "echarts";
import { chartDataList } from "../../utils/dataList";
const props = defineProps({
  sortType: {
    type: String,
  },
});
const pieChart = ref<HTMLElement>();
const myChart2 = ref<any>();
const hours = [
  "B Cell1",
  "B Cell2",
  "B Cell3",
  "B Cell4",
  "B Cell5",
  "B Cell6",
  "B Cell7",
  "B Cell8",
  "B Cell9",
  "B Cell10",
  "B Cell11",
  "B Cell12",
  "B Cell13",
  "B Cell14",
  "B Cell15",
  "B Cell16",
  "B Cell17",
  "B Cell18",
  "B Cell19",
  "B Cell20",
  "B Cell21",
  "B Cell22",
  "B Cell23",
  "B Cell24",
];
// prettier-ignore
const days = [
    'gene1', 'gene2', 'gene3',
    'gene4', 'gene5', 'gene6', 'gene7','gene8','gene9','gene10','gene11','gene12','gene13'
];

const initPieEcharts = () => {
  myChart2.value = echarts.init(pieChart.value!);
  myChart2.value.setOption({
    tooltip: {
      position: "top",
    },
    toolbox: {
      show: true,
      feature: {
        mark: { show: true },
        dataView: { show: true, readOnly: false },
        restore: { show: true },
        saveAsImage: { show: true },
      },
    },
    grid: {
      height: "50%",
      top: "10%",
    },
    xAxis: {
      axisLabel: {
        interval: 0,
        rotate: 40,
      },
      type: "category",
      data: hours,
      splitArea: {
        show: true,
      },
    },
    yAxis: {
      type: "category",
      data: days,
      splitArea: {
        show: true,
      },
    },
    visualMap: {
      min: 0,
      max: 10,
      calculable: true,
      orient: "horizontal",
      left: "center",
      bottom: "15%",
    },
    series: [
      {
        name: "Punch Card",
        type: "heatmap",
        data: chartDataList,
        label: {
          show: true,
        },
        emphasis: {
          itemStyle: {
            shadowBlur: 10,
            shadowColor: "rgba(0, 0, 0, 0.5)",
          },
        },
      },
    ],
  });
};
onMounted(() => {
  initPieEcharts();
});
</script>
<style scoped lang="scss"></style>
