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

// Fixed: variable name and proper initialization
const selectedChat = ref(null);

// Fixed: handler name matches the event emitted from ChatList component
const handleSelectChat = (chat) => {
  selectedChat.value = chat;
};
</script>

<template>
  <div class="max-w-[1380px] mx-auto px-2 md:px-0">
    <div class="flex flex-col md:flex-row gap-12">
      <div class="w-full md:w-1/3">
        <Conversation />
        <!-- Fixed: event name matches the handler function -->
        <ChatList @select-chat="handleSelectChat" />
      </div>
      <div class="w-full md:w-2/3">
        <!-- Fixed: prop name matches the component expectation -->
        <ChatDetail :conversation="selectedChat" />
      </div>
    </div>
  </div>
</template>
