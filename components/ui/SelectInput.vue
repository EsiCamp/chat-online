<script setup>
defineProps({
  options: {
    type: Array,
    required: true,
  },
  modelValue: {
    type: [String, Number],
    default: "",
  },
  placeholder: {
    type: String,
    required: true,
  },
  label: {
    type: String,
    default: "",
  },
});

defineEmits(["update:modelValue"]);
</script>

<template>
  <div class="w-full">
    <label v-if="label" class="block mb-1 text-sm font-medium">{{
      label
    }}</label>
    <select
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      class="w-full px-2 py-1.5 border border-[#dcdcdc] rounded-lg text-sm text-[#777]"
      :aria-label="label || placeholder"
    >
      <option disabled value="">{{ placeholder }}</option>
      <option v-for="option in options" :key="option.id" :value="option.id">
        {{ option.name }}
      </option>
    </select>
  </div>
</template>
