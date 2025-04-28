<script setup>
defineProps({
  chat: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div
    class="flex flex-col md:flex-row items-center gap-2 p-4 border-b border-gray-100 hover:bg-gray-50 transition-colors"
  >
    <!-- Avatar Section -->
    <div class="w-full md:w-1/4 flex justify-center mb-4 md:mb-0">
      <div
        class="grid place-items-center w-[80px] h-[80px] rounded-full"
        :style="{ backgroundColor: chat.avatarColor || '#0066ff' }"
      >
        <span class="text-white text-lg font-medium">{{ chat.initials }}</span>
      </div>
    </div>

    <!-- Content Section -->
    <div class="w-full md:w-3/4 flex flex-col gap-y-3">
      <!-- Tags -->
      <div class="flex gap-x-1">
        <span
          class="bg-[#d2e5cc] text-sm text-[#638657] rounded-lg px-2 py-0.5 w-1/3 text-center truncate"
          >{{ chat.website }}</span
        >
        <span
          class="bg-[#d2e5cc] text-sm text-[#638657] rounded-lg px-2 py-0.5 w-1/3 text-center truncate"
          >{{ chat.department }}</span
        >
        <span
          class="bg-[#d2e5cc] text-sm text-[#638657] rounded-lg px-2 py-0.5 w-1/3 text-center truncate"
          >{{ chat.operator }}</span
        >
      </div>

      <!-- Name and Unread Count -->
      <div class="flex justify-between items-center">
        <span class="font-bold">{{ chat.name }}</span>
        <span
          v-if="chat.unreadCount > 0"
          class="rounded-full text-white bg-[#0066ff] px-2 py-0.5 text-xs min-w-[20px] text-center"
          >{{ chat.unreadCount }}</span
        >
      </div>

      <!-- Last Message and Time -->
      <div class="flex justify-between items-center">
        <span class="font-semibold text-sm text-[#999] truncate max-w-[70%]">{{
          chat.lastMessage
        }}</span>
        <time :datetime="chat.dateIso" class="text-[#999] text-sm">{{
          chat.formattedDate
        }}</time>
      </div>
    </div>
  </div>
</template>
