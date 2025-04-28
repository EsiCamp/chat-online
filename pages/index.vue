<script setup>
import { defineAsyncComponent, ref } from "vue";

const Conversation = defineAsyncComponent(() =>
  import("~/components/list/ConversationCmp.vue")
);
const ChatList = defineAsyncComponent(() =>
  import("~/components/list/ChatList.vue")
);
const ChatDetail = defineAsyncComponent(() =>
  import("~/components/chat/ChatDetail.vue")
);

const selectedChat = ref(null);

const handleSelectChat = (chat) => {
  selectedChat.value = chat;
};
</script>

<template>
  <div class="max-w-[1380px] mx-auto px-2 md:px-0 py-16">
    <div class="flex flex-col md:flex-row gap-12">
      <div class="w-full md:w-1/3">
        <Conversation />
        <ChatList @select-chat="handleSelectChat" />
      </div>
      <div class="w-full md:w-2/3 md:border-r md:border-[#dcdcdc] md:pr-6">
        <ChatDetail :conversation="selectedChat" />
      </div>
    </div>
  </div>
</template>
