<template>
  <div class="flex justify-center w-auto">
    <div class="block p-1 rounded-lg shadow-lg bg-white max-w-lg">
      <div>
        <h5
          class="text-xl text-2xl font-mono text-left text-indigo-900 leading-tight font-medium mb-2"
        >
          <app-title></app-title>
        </h5>
      </div>
      <div class="bg-indigo-900 p-5 center-item">
        <app-chart :chartData="chartData"></app-chart>
      </div>
      <div class="flex justify-between mt-10 divide-x">
        <app-button></app-button>
        <app-textField @fetchedDataset="fetchDataset"></app-textField>
      </div>
    </div>
  </div>
</template>

<script>
import Title from "../title/Title.vue";
import Chart from "../chart/Chart.vue";
import Button from "../buttons/Button.vue";
import TextField from "../inputField/TextField.vue";
export default {
  data: function () {
    return {
      chartData: {
        mean: 0,
        median: 0,
        stdDeviation: 0,
        mode: 0,
      },
    };
  },
  methods: {
    fetchDataset(results) {
      this.chartData = {
        ...this.chartData,
        ...results,
      };
    },
  },
  components: {
    "app-title": Title,
    "app-chart": Chart,
    "app-button": Button,
    "app-textField": TextField,
  },
};
</script>
