<script setup>
import { defineAsyncComponent, ref, watch } from "vue";

const ChatMessage = defineAsyncComponent(() =>
  import("~/components/chat/ChatMessage.vue")
);

const props = defineProps({
  conversation: {
    type: Object,
    required: true,
  },
});

const messages = ref([]);

watch(
  () => props.conversation,
  (newConversation) => {
    if (!newConversation) return;

    const sampleMessages = [];

    sampleMessages.push({
      id: 1,
      senderId: "system",
      content: `به گفتگو با ${newConversation.name} خوش آمدید.`,
      dateIso: newConversation.dateIso,
      formattedTime: "۰۹:۳۰",
      isSystem: true,
    });

    sampleMessages.push({
      id: 2,
      senderId: newConversation.id,
      content: newConversation.lastMessage,
      dateIso: newConversation.dateIso,
      formattedTime: newConversation.formattedDate.split(" ")[1],
      isSystem: false,
    });

    sampleMessages.push({
      id: 3,
      senderId: "operator",
      content: `سلام ${newConversation.name}، چطور می‌توانم به شما کمک کنم؟`,
      dateIso: new Date(
        new Date(newConversation.dateIso).getTime() + 5 * 60000
      ).toISOString(),
      formattedTime: "۱۱:۴۰",
      isSystem: false,
    });

    if (newConversation.department === "پشتیبانی") {
      sampleMessages.push({
        id: 4,
        senderId: newConversation.id,
        content: "من مشکلی در سایت دارم. صفحه پرداخت کار نمی‌کند.",
        dateIso: new Date(
          new Date(newConversation.dateIso).getTime() + 10 * 60000
        ).toISOString(),
        formattedTime: "۱۱:۴۵",
        isSystem: false,
      });

      sampleMessages.push({
        id: 5,
        senderId: "operator",
        content:
          "متوجه شدم. لطفاً مرورگر خود را به‌روزرسانی کنید و دوباره امتحان کنید. اگر مشکل برطرف نشد، به من اطلاع دهید.",
        dateIso: new Date(
          new Date(newConversation.dateIso).getTime() + 15 * 60000
        ).toISOString(),
        formattedTime: "۱۱:۵۰",
        isSystem: false,
      });
    } else if (newConversation.department === "فروش") {
      sampleMessages.push({
        id: 4,
        senderId: newConversation.id,
        content: "آیا محصول جدید شما در انبار موجود است؟",
        dateIso: new Date(
          new Date(newConversation.dateIso).getTime() + 10 * 60000
        ).toISOString(),
        formattedTime: "۱۱:۴۵",
        isSystem: false,
      });

      sampleMessages.push({
        id: 5,
        senderId: "operator",
        content:
          "بله، در حال حاضر موجود است. می‌توانید آن را از طریق وب‌سایت سفارش دهید.",
        dateIso: new Date(
          new Date(newConversation.dateIso).getTime() + 15 * 60000
        ).toISOString(),
        formattedTime: "۱۱:۵۰",
        isSystem: false,
      });
    }

    messages.value = sampleMessages;
  },
  { immediate: true }
);

const newMessage = ref("");
const sendMessage = () => {
  if (!newMessage.value.trim()) return;

  messages.value.push({
    id: Date.now(),
    senderId: "operator",
    content: newMessage.value,
    dateIso: new Date().toISOString(),
    formattedTime: new Date().toLocaleTimeString("fa-IR", {
      hour: "2-digit",
      minute: "2-digit",
    }),
    isSystem: false,
  });

  newMessage.value = "";
};
</script>

<template>
  <div v-if="conversation" class="flex flex-col h-full">
    <div class="bg-white p-4 border-b">
      <div class="flex items-center gap-3">
        <div
          class="grid place-items-center w-[40px] h-[40px] rounded-full"
          :style="{ backgroundColor: conversation.avatarColor || '#0066ff' }"
        >
          <span class="text-white text-sm">{{ conversation.initials }}</span>
        </div>
        <div>
          <div class="font-bold">{{ conversation.name }}</div>
          <div class="text-sm text-gray-500">
            {{ conversation.department }} • {{ conversation.website }}
          </div>
        </div>
      </div>
    </div>

    <div class="flex-1 overflow-y-auto p-4 bg-gray-50 flex flex-col">
      <div v-for="message in messages" :key="message.id">
        <div v-if="message.isSystem" class="text-center my-4">
          <span
            class="bg-gray-200 text-gray-600 px-3 py-1 rounded-full text-xs"
          >
            {{ message.content }}
          </span>
        </div>

        <ChatMessage
          v-else
          :message="message"
          :isOwn="message.senderId === 'operator'"
        />
      </div>
    </div>

    <div class="bg-white p-3 border-t">
      <div class="flex gap-2">
        <input
          v-model="newMessage"
          type="text"
          placeholder="پیام خود را بنویسید..."
          class="flex-1 border border-gray-300 rounded-lg px-3 py-2"
          @keyup.enter="sendMessage"
        />
        <button
          @click="sendMessage"
          class="bg-[#0066ff] text-white px-4 py-2 rounded-lg"
        >
          ارسال
        </button>
      </div>
    </div>
  </div>

  <div v-else class="flex items-center justify-center h-full bg-gray-50">
    <div class="text-center text-gray-500">
      <p>یک گفتگو را انتخاب کنید</p>
    </div>
  </div>
</template>
