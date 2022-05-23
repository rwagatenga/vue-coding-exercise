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
        @click="fetchDataset(results)"
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
      results: {},
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
          this.dataSets = Object.values(response.data.data);
          for (const key in response.data.data) {
            sum += parseFloat(response.data.data[key]);
          }

          const median = (medianArr) => {
            const mid = Math.floor(medianArr.length / 2),
              nums = [...medianArr].sort((a, b) => a - b);
            return medianArr.length % 2 !== 0
              ? nums[mid]
              : (nums[mid - 1] + nums[mid]) / 2;
          };

          const stdDeviation = (arr) => {
            // Creating the mean with Array.reduce
            let mean =
              arr.reduce((acc, curr) => {
                return parseFloat(acc) + parseFloat(curr);
              }, 0) / arr.length;

            // Assigning (value - mean) ^ 2 to every array item
            arr = arr.map((k) => {
              return (parseFloat(k) - mean) ** 2;
            });

            // Calculating the sum of updated array
            let sum = arr.reduce(
              (acc, curr) => parseFloat(acc) + parseFloat(curr),
              0
            );

            // Returning the Standered deviation
            return Math.sqrt(sum / arr.length);
          };

          const mode = (modeArray) => {
            return modeArray.reduce(
              function (current, num) {
                const freq =
                  num in current.numMap
                    ? ++current.numMap[num]
                    : (current.numMap[num] = 1);
                if (freq > current.modeFreq && freq > 1) {
                  current.modeFreq = freq;
                  current.mode = num;
                }
                return current;
              },
              { mode: null, modeFreq: 0, numMap: {} }
            ).mode;
          };
          this.results = {
            ...this.results,
            mean: parseFloat(sum / NumberOfKeys).toFixed(2),
            median: median(Object.values(response.data.data)),
            stdDeviation: stdDeviation(
              Object.values(response.data.data)
            ).toFixed(2),
            mode: mode(Object.values(response.data.data)),
          };
          this.$emit("fetchedDataset", this.results);
          this.insertURL = "";
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
