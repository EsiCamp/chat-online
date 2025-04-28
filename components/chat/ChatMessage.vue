<script setup>
defineProps({
  message: {
    type: Object,
    required: true,
  },
  isOwn: {
    type: Boolean,
    default: false,
  },
});
</script>

<template>
  <div :class="['mb-4 max-w-[80%]', isOwn ? 'self-end' : 'self-start']">
    <div
      :class="[
        'rounded-lg px-4 py-2',
        isOwn ? 'bg-[#0066ff] text-white' : 'bg-gray-100 text-gray-800',
      ]"
    >
      <p class="whitespace-pre-wrap">{{ message.content }}</p>
    </div>

    <div
      :class="[
        'text-xs mt-1 text-gray-500',
        isOwn ? 'text-left' : 'text-right',
      ]"
    >
      <time :datetime="message.dateIso">{{ message.formattedTime }}</time>
    </div>
  </div>
</template>
