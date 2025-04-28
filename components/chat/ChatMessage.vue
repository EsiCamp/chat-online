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
  sender: {
    type: Object,
    default: () => ({}),
  },
  operator: {
    type: Object,
    default: () => ({
      initials: "اپ",
      avatarColor: "#0066ff",
    }),
  },
});
</script>

<template>
  <div
    :class="[
      'mb-4 flex items-start gap-2',
      isOwn ? 'self-end' : 'self-start flex-row-reverse',
    ]"
  >
    <div v-if="isOwn" class="flex-shrink-0">
      <div
        class="grid place-items-center w-[32px] h-[32px] rounded-full"
        :style="{ backgroundColor: operator.avatarColor || '#0066ff' }"
      >
        <span class="text-white text-xs">{{ operator.initials }}</span>
      </div>
    </div>

    <div class="flex flex-col">
      <div
        :class="[
          'rounded-lg px-4 py-2',
          isOwn
            ? 'bg-gray-100 text-gray-800 rounded-tl-none'
            : 'bg-[#0066ff] text-white rounded-tr-none',
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
  </div>
</template>
