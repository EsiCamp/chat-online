<script setup>
import { ref, defineAsyncComponent } from "vue";

const SelectInput = defineAsyncComponent(() =>
  import("~/components/ui/SelectInput.vue")
);
const DateTimePicker = defineAsyncComponent(() =>
  import("~/components/ui/DateTimePicker.vue")
);
const SearchInput = defineAsyncComponent(() =>
  import("~/components/ui/SearchInput.vue")
);

const websites = ref([
  { id: 1, name: "وبسایت اصلی" },
  { id: 2, name: "فروشگاه آنلاین" },
  { id: 3, name: "بلاگ" },
  { id: 4, name: "پورتال مشتریان" },
]);

const departments = ref([
  { id: 1, name: "فروش" },
  { id: 2, name: "پشتیبانی" },
  { id: 3, name: "فنی" },
  { id: 4, name: "بازاریابی" },
  { id: 5, name: "مالی" },
]);

const operators = ref([
  { id: 1, name: "سوالات متداول" },
  { id: 2, name: "گزارش مشکل" },
  { id: 3, name: "پیشنهادات" },
  { id: 4, name: "شکایات" },
]);

const selectedWebsite = ref("");
const selectedDepartment = ref("");
const selectedOperator = ref("");
const selectedDateTime = ref("");
const searchQuery = ref("");
</script>

<template>
  <div class="flex flex-col gap-y-4 mb-4">
    <h2 class="font-bold">گفتگو</h2>

    <div class="flex gap-2">
      <SelectInput
        v-model="selectedWebsite"
        :options="websites"
        placeholder="انتخاب وب‌سایت"
        class="w-1/2"
      />

      <SelectInput
        v-model="selectedDepartment"
        :options="departments"
        placeholder="انتخاب دپارتمان"
        class="w-1/2"
      />
    </div>

    <div class="flex gap-2">
      <SelectInput
        v-model="selectedOperator"
        :options="operators"
        placeholder="انتخاب اپراتور"
        class="w-1/2"
      />

      <DateTimePicker
        v-model="selectedDateTime"
        placeholder="انتخاب تاریخ"
        class="w-1/2"
      />
    </div>

    <div class="flex gap-2">
      <SearchInput
        v-model="searchQuery"
        placeholder="کلمه کلیدی جستچو را وارد کنید"
      />

      <button class="w-1/2 bg-[#0066ff] text-white rounded-lg cursor-pointer">
        جستجو
      </button>
    </div>
  </div>
</template>
