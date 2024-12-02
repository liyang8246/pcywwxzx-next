<script setup>
import { ref } from 'vue';

const datesList = ref([]);
const dateModel = defineModel();

const getDatesRange = (currentDate, days) => {
  const dates = [];
  const weekdays = ['周日', '周一', '周二', '周三', '周四', '周五', '周六'];
  for (let i = 0; i < days; i++) {
    const date = new Date(currentDate);
    date.setDate(currentDate.getDate() + i);
    if (date.getDay() === 0 || date.getDay() === 6) {
      days += 1;
      continue;
    }
    dates.push({
      date: date,
      year: date.getFullYear(),
      month: date.getMonth() + 1,
      day: date.getDate(),
      weekday: weekdays[date.getDay()],
    });
  }
  return dates;
};

datesList.value = getDatesRange(new Date(), 5);
const selectDate = (date) => {
  dateModel.value = new Date(date.date.getTime() + 8 * 3600000).toISOString().slice(0, 10) + 'T00:00:00.000000000';
};
</script>

<template>
  <!-- <div class="input p-0 join max-w-full h-9 ">
        <label v-for="date in datesList" :key="date"
            class="flex justify-center items-center w-full join-item rounded cursor-pointer bg-base-200 has-[:checked]:bg-primary">
            <input type="radio" name="DateOption" :value="date" :id="date" @change="selectDate(date)" class="sr-only" />
            <p class="text-base-content"> {{ date.day }} </p>
            <p class="text-xs mt-2 text-base-content"> {{ '/' + date.weekday }} </p>
        </label>
    </div> -->
  <div class="p-0 join max-w-full flex">
    <input
      v-for="date in datesList"
      :key="date"
      name="DateOption"
      :value="date"
      :id="date"
      @change="selectDate(date)"
      class="join-item btn flex-grow p-0 text-sm"
      type="radio"
      :aria-label="date.day + '/' + date.weekday"
    />
  </div>
</template>
