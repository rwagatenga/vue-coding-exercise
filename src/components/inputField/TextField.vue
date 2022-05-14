<template>
  <div class="items-center p-5">
    <div class="m-0 flex">
      <input
        class="rounded-l-lg p-2 border-t mr-0 border-b border-l text-gray-800 border-gray-200 bg-white"
        placeholder="URL"
        v-model="insertURL"
      />
      <button
        class="px-5 rounded-r-lg bg-indigo-900 hover:bg-indigo-800 text-white font-bold p-2 uppercase border-indigo-800 border-t border-b border-r"
        @click="fetchDataset"
      >
        Fetch
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import math from "mathjs";
export default {
  data: function () {
    return {
      insertURL: "",
      dataSets: [],
      mean: 0,
      median: 0,
      stdDeviation: 0,
    };
  },
  methods: {
    fetchDataset() {
      axios
        .get(this.insertURL)
        .then((response) => {
          let sum = 0;
          let NumberOfKeys = Object.keys(response.data.data).length;
          this.dataSets = Object.values(response.data.data)
          for (const key in response.data.data) {
            sum += parseFloat(response.data.data[key]);
          }
          this.mean = parseFloat(sum / NumberOfKeys).toFixed(2);
          const median = (medianArr) => {
            const mid = Math.floor(medianArr.length / 2),
              nums = [...medianArr].sort((a, b) => a - b);
            return medianArr.length % 2 !== 0
              ? nums[mid]
              : (nums[mid - 1] + nums[mid]) / 2;
          };
          this.median = median(this.dataSets);
          this.stdDeviation = math.std(this.dataSets);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
