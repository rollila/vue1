<script setup>
import { reactive } from "vue";

import Cell from "./components/cell.vue";

const state = reactive({
  numRows: 5,
  selectedCells: {},
  isMouseDown: false
});

const selectCell = (i, n) => {
  state.selectedCells[`${i}-${n}`] = state.selectedCells[`${i}-${n}`] ? false : true
}
</script>

<template>
  <div class="flex justify-center bg-gray-50 min-h-screen">
    <div class="w-[1200px] max-w-[1200px] space-y-8 bg-white">
      <div class="p-8">
        <label class="font-bold">Number of rows</label>
        <input
          class="block p-2 border-neutral-600 rounded border-solid border"
          type="number"
          v-model="state.numRows"
        />
      </div>
      <div class="p-8">
        <div
          v-for="(row, i) in state.numRows"
          :key="i"
          class="flex items-center"
        >
          <cell
            v-for="n in 25"
            @select="selectCell(i, n)"
            @mdown="state.isMouseDown = true"
            @mup="state.isMouseDown = false"
            :key="n"
            class="flex-grow basis-0"
            :is-mouse-down="state.isMouseDown"
          />
        </div>
      </div>
    </div>
  </div>
</template>
