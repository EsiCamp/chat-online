<script setup>
import { defineAsyncComponent } from "vue";

const Conversation = defineAsyncComponent(() =>
  import("~/components/list/ConversationCmp.vue")
);
const ChatList = defineAsyncComponent(() =>
  import("~/components/list/ChatList.vue")
);
</script>

<template>
  <div class="max-w-[1380px] mx-auto px-2 md:px-0">
    <div class="flex flex-col md:flex-row gap-6">
      <div class="w-full md:w-1/3">
        <Conversation />
        <ChatList />
      </div>
    </div>
  </div>
</template>
