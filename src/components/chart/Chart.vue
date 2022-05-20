<template>
  <div class="grid grid-cols-4 gap-4">
    <div>
      <div
        class="rounded-full bg-white items-center place-items-center text-center w-24 h-24 p-8"
      >
        <span class="text-center font-medium">{{ chartData.mean }}</span>
      </div>
      <div class="text-center text-white mt-2 font-medium text-sm">Mean</div>
    </div>
    <div>
      <div
        class="rounded-full bg-white items-center place-items-center text-center w-24 h-24 p-8"
      >
        <span class="text-center font-medium">{{ chartData.median }}</span>
      </div>
      <div class="text-center text-white mt-2 font-medium text-sm">Median</div>
    </div>
    <div>
      <div
        class="rounded-full bg-white items-center place-items-center text-center w-24 h-24 p-8"
      >
        <span class="text-center font-medium">{{
          chartData.stdDeviation
        }}</span>
      </div>
      <div class="text-center text-white mt-2 font-medium text-sm">
        STD Deviation
      </div>
    </div>
    <div>
      <div
        class="rounded-full bg-white items-center place-items-center text-center w-24 h-24 p-8"
      >
        <span class="text-center font-medium">{{ chartData.mode }}</span>
      </div>
      <div class="text-center text-white mt-2 font-medium text-sm">Mode</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    chartData: {
      mean: {
        type: Number,
        required: true,
      },
      median: {
        type: Number,
        required: true,
      },
      stdDeviation: {
        type: Number,
        required: true,
      },
      mode: {
        type: Number,
        required: true,
      },
    },
  },
};
</script>
