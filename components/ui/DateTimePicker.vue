<script setup>
import { ref } from "vue";

const props = defineProps({
  modelValue: {
    type: String,
    default: "",
  },
  placeholder: {
    type: String,
    default: "انتخاب تاریخ",
  },
  label: {
    type: String,
    default: "",
  },
});

const emit = defineEmits(["update:modelValue"]);
const dateTimeInput = ref(null);

const openDateTimePicker = () => {
  if (dateTimeInput.value) {
    dateTimeInput.value.focus();
    dateTimeInput.value.click();
  }
};

const formattedDate = () => {
  if (!props.modelValue) return "";
  const date = new Date(props.modelValue);
  return date.toLocaleString("fa-IR");
};
</script>

<template>
  <div class="w-full">
    <label v-if="label" class="block mb-1 text-sm font-medium">{{
      label
    }}</label>
    <div class="relative w-full border border-[#dcdcdc] rounded-lg">
      <div class="relative w-full h-9 flex items-center">
        <div v-if="!modelValue" class="absolute px-3 text-sm text-[#777]">
          {{ placeholder }}
        </div>

        <div
          v-else
          class="px-3 text-sm overflow-hidden text-ellipsis whitespace-nowrap"
        >
          {{ formattedDate() }}
        </div>

        <button
          type="button"
          class="absolute left-2 top-1/2 transform -translate-y-1/2 text-[#777] border-none bg-transparent cursor-pointer z-10"
          @click="openDateTimePicker"
          :aria-label="placeholder"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="20"
            height="20"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-calendar"
          >
            <rect x="3" y="4" width="18" height="18" rx="2" ry="2"></rect>
            <line x1="16" y1="2" x2="16" y2="6"></line>
            <line x1="8" y1="2" x2="8" y2="6"></line>
            <line x1="3" y1="10" x2="21" y2="10"></line>
          </svg>
        </button>
      </div>

      <input
        ref="dateTimeInput"
        :value="modelValue"
        @input="emit('update:modelValue', $event.target.value)"
        type="datetime-local"
        class="absolute inset-0 opacity-0 cursor-pointer"
        :aria-label="placeholder"
      />
    </div>
  </div>
</template>
