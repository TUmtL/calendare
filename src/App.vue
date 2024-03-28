<template>
  <div class="container">
    <button
      class="lang-btn"
      @click="lang == 'ru' ? (lang = 'eng') : (lang = 'ru')"
    >
      {{ lang }}
    </button>
    <p class="year">
      <span @click="curentDate.year--">-</span>{{ curentDate.year }}
      <span @click="curentDate.year++">+</span>
    </p>
    <p class="month">
      <span @click="monthF('-')">-</span>
      <span v-if="lang == 'ru'">{{
        months.ru.monthLocalization[curentDate.month]
      }}</span>
      <span v-if="lang == 'eng'">{{
        months.eng.monthLocalization[curentDate.month]
      }}</span>
      <span @click="monthF('+')">+</span>
    </p>
    <div class="week-day">
      <div v-if="lang == 'ru'" v-for="one of months.ru.weekDayLocalization" class="day">
        {{ one }}
      </div>
      <div v-if="lang == 'eng'" v-for="one of months.eng.weekDayLocalization" class="day">
        {{ one }}
      </div>
    </div>
    <div class="calendars-day">
      <div @click="console.log(new Date(`${curentDate.year} ${curentDate.month + 1} ${one}`))" v-for="one of monthsDays[curentDate.month]" :key="one" class="day">
        {{ one }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";
const lang = ref("ru");

const dateString = ref(Date(Date.now()));
const curentDate = ref({
  day: new Date(dateString.value).getDate(),
  month: new Date(dateString.value).getMonth(),
  weekDay: new Date(dateString.value).getDay(),
  year: new Date(dateString.value).getFullYear(),
});
const monthFirstDay = computed(() => {
  return new Date(
    `${curentDate.value.year} ${curentDate.value.month + 1} 1`
  ).getDay();
});
function monthF(param) {
  if (param == "+") {
    if (curentDate.value.month >= 11) {
      curentDate.value.month = 0;
    } else {
      curentDate.value.month += 1;
    }
  }
  if (param == "-") {
    if (curentDate.value.month <= 0) {
      curentDate.value.month = 11;
    } else {
      curentDate.value.month -= 1;
    }
  }
}
watch(
  () => curentDate,
  () => {
    // if (curentDate.value[curentDate.value.month] != null) {
    monthsDays.value[curentDate.value.month] = monthsDays.value[
      curentDate.value.month
    ].filter((el) => el != " ");
    for (let i = 1; i < monthFirstDay.value; i++) {
      monthsDays.value[curentDate.value.month].unshift(" ");
    }
    // }
  },
  { deep: true }
);
const februaryDays = computed(() => {
  if (curentDate.value.year % 4 == 0) {
    return [
      1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
      22, 23, 24, 25, 26, 27, 28, 29,
    ];
  } else {
    return [
      1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
      22, 23, 24, 25, 26, 27, 28,
    ];
  }
});
const monthsDays = ref([
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
  februaryDays.value,
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30,
  ],
  [
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31,
  ],
]);
console.log(monthsDays.value[0]);

const months = ref({
  ru: {
    monthLocalization: [
      "Январь",
      "февраль",
      "Март",
      "Апрель",
      "Май",
      "Июнь",
      "Июль",
      "Август",
      "Сентябрь",
      "Октябрь",
      "Ноябрь",
      "Декабрь",
    ],
    weekDayLocalization: [
      "понедельник",
      "вторник",
      "среда",
      "четверг",
      "пятница",
      "суббота",
      "воскресенье",
    ],
  },
  eng: {
    monthLocalization: [
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December",
    ],
    weekDayLocalization: [
      "Monday,",
      "Tuesday",
      "Wednesday",
      "Thursday",
      "Friday",
      "Saturday",
      "Sunday",
    ],
  },
});
// const monthTasks = ref([{day:'test' , task:'test'}] ,[] ,[] ,[] ,[] ,[] ,[] ,[] ,[] ,[] ,[] ,[])
monthsDays.value[curentDate.value.month] = monthsDays.value[
  curentDate.value.month
].filter((el) => el != " ");
for (let i = 1; i < monthFirstDay.value; i++) {
  monthsDays.value[curentDate.value.month].unshift(" ");
}
</script>

<style>
.calendars-day,
.week-day {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
}
</style>