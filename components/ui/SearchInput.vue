<script setup>
defineProps({
  modelValue: {
    type: String,
    default: "",
  },
  placeholder: {
    type: String,
    default: "جستجو...",
  },
  label: {
    type: String,
    default: "",
  },
});

defineEmits(["update:modelValue"]);
</script>

<template>
  <div class="w-1/2">
    <label v-if="label" class="block mb-1 text-sm font-medium">{{
      label
    }}</label>
    <div class="relative w-full">
      <input
        type="text"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :placeholder="placeholder"
        class="w-full py-1.5 px-7 border border-[#dcdcdc] rounded-lg text-sm text-[#777]"
        :aria-label="placeholder"
      />
      <span class="absolute right-[6px] top-[12px]">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          viewBox="0 0 24 24"
        >
          <path
            fill="none"
            stroke="#666"
            stroke-linecap="round"
            stroke-width="2"
            d="m21 21l-4.486-4.494M19 10.5a8.5 8.5 0 1 1-17 0a8.5 8.5 0 0 1 17 0Z"
          />
        </svg>
      </span>
    </div>
  </div>
</template>
