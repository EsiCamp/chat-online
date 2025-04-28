<script setup>
import { defineAsyncComponent, ref, computed } from "vue";

const ChatItem = defineAsyncComponent(() =>
  import("~/components/list/ChatItem.vue")
);

const chatsData = ref([
  {
    id: 1,
    name: "آرین بهرامی",
    initials: "آ.ب",
    avatarColor: "#0066ff",
    website: "aaaaa.com",
    department: "پشتیبانی",
    operator: "علی محمدی",
    lastMessage: "سلام و وقت بخیر",
    dateIso: "2025-04-28T11:35:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۸ ۱۱:۳۵",
    unreadCount: 3,
  },
  {
    id: 2,
    name: "نیما حسینی",
    initials: "ن.ح",
    avatarColor: "#ff6600",
    website: "example.com",
    department: "فروش",
    operator: "سارا احمدی",
    lastMessage: "میخواستم درباره محصول جدید سوال کنم",
    dateIso: "2025-04-28T10:22:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۸ ۱۰:۲۲",
    unreadCount: 1,
  },
  {
    id: 3,
    name: "مهسا صادقی",
    initials: "م.ص",
    avatarColor: "#33cc66",
    website: "store.example.com",
    department: "فنی",
    operator: "مهدی رضایی",
    lastMessage: "مشکل من حل شد، ممنون از راهنمایی شما",
    dateIso: "2025-04-28T09:15:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۸ ۰۹:۱۵",
    unreadCount: 0,
  },
  {
    id: 4,
    name: "فاطمه محمدی",
    initials: "ف.م",
    avatarColor: "#9966cc",
    website: "blog.example.com",
    department: "بازاریابی",
    operator: "حسین کریمی",
    lastMessage: "لطفا محتوای جدید را بررسی کنید",
    dateIso: "2025-04-27T16:40:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۷ ۱۶:۴۰",
    unreadCount: 5,
  },
  {
    id: 5,
    name: "علی رضایی",
    initials: "ع.ر",
    avatarColor: "#cc3366",
    website: "support.example.com",
    department: "مالی",
    operator: "زهرا کاظمی",
    lastMessage: "فاکتور ماه گذشته ارسال شد",
    dateIso: "2025-04-27T14:05:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۷ ۱۴:۰۵",
    unreadCount: 0,
  },
  {
    id: 6,
    name: "سارا مرادی",
    initials: "س.م",
    avatarColor: "#3399ff",
    website: "portal.example.com",
    department: "پشتیبانی",
    operator: "رضا فرهادی",
    lastMessage: "سفارش من هنوز ارسال نشده است",
    dateIso: "2025-04-27T11:20:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۷ ۱۱:۲۰",
    unreadCount: 2,
  },
  {
    id: 7,
    name: "محمد احمدی",
    initials: "م.ا",
    avatarColor: "#ff9900",
    website: "shop.example.com",
    department: "فروش",
    operator: "نرگس اکبری",
    lastMessage: "میخواستم از تخفیف ویژه استفاده کنم",
    dateIso: "2025-04-26T17:30:00Z",
    formattedDate: "۱۴۰۳/۰۸/۰۶ ۱۷:۳۰",
    unreadCount: 0,
  },
]);

const sortedChats = computed(() => {
  return [...chatsData.value].sort((a, b) => {
    if (a.unreadCount > 0 && b.unreadCount === 0) return -1;
    if (a.unreadCount === 0 && b.unreadCount > 0) return 1;
    return new Date(b.dateIso) - new Date(a.dateIso);
  });
});

const selectedChat = ref(null);
const emit = defineEmits(["select-chat"]);

const handleSelect = (chat) => {
  selectedChat.value = chat;
  emit("select-chat", chat);
};
</script>

<template>
  <div>
    <div class="max-h-[600px] overflow-y-auto">
      <div
        v-if="sortedChats.length === 0"
        class="p-6 text-center text-gray-500"
      >
        گفتگویی یافت نشد
      </div>
      <div v-else>
        <div
          v-for="chat in sortedChats"
          :key="chat.id"
          @click="handleSelect(chat)"
          :class="[
            'cursor-pointer',
            selectedChat?.id === chat.id ? 'bg-blue-50' : '',
          ]"
        >
          <ChatItem :chat="chat" />
        </div>
      </div>
    </div>
  </div>
</template>
