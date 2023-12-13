<script setup lang="ts">
import { reactive } from "vue";

const props = defineProps<{
  isMouseDown: boolean
}>()

const state = reactive({
  selected: false,
});

const emit = defineEmits<{
  (e: "select"): void;
  (e: "mdown"): void;
  (e: "mup"): void;
}>();

const onSelect = () => {
  state.selected = !state.selected;
  emit("select");
};

const onMouseEnter = () => {
  if (props.isMouseDown) onSelect()
}
</script>

<template>
  <div
    @click="onSelect"
    @mouseenter="onMouseEnter"
    @mousedown="emit('mdown')"
    @mouseup="emit('mup')"
    class="p-2 rounded border-gray-200 border border-solid h-10 hover:bg-teal-100"
    :class="state.selected ? 'bg-green-100' : null"
  />
</template>
