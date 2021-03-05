<template>
  <div>
    <div class="header">
      <div class="container">
        <h1 class="title">เราคบกันมาแล้ว</h1>
        <h2 class="subtitle">เพราะความรักคือการดูแลกัน ไม่ใช่การจำวันครบรอบ</h2>
      </div>
    </div>
    <div class="container">
      <div class="datetime">
        <div class="date">
          <ul>
            <li>
              {{ state.year }}
              <span class="unit">ปี</span>
            </li>
            <li>{{ state.month }} <span class="unit">เดือน</span></li>
            <li>{{ state.day }} <span class="unit">วัน</span></li>
          </ul>
        </div>
        <div class="time">
          <ul>
            <li>{{ state.hour }} <span class="unit">ชั่วโมง</span></li>
            <li>{{ state.minute }} <span class="unit">นาที</span></li>
            <li>{{ state.second }} <span class="unit">วินาที</span></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, reactive } from "vue";
// import anime from "animejs/lib/anime.es";

export default {
  setup() {
    const dayjs = require("dayjs");

    const state = reactive({
      year: 0,
      month: 0,
      day: 0,
      hour: 0,
      minute: 0,
      second: 0,
    });

    const differ = () => {
      const customParseFormat = require("dayjs/plugin/customParseFormat");
      dayjs.extend(customParseFormat);

      const start = dayjs("2021-01-30");

      state.year = dayjs().diff(start, "year");
      state.month = dayjs().diff(start, "month") % 12;
      state.day = dayjs().diff(start, "day") % 30;
    };

    const timer = () => {
      state.hour = dayjs().format("H");
      state.minute = dayjs().format("m");
      state.second = dayjs().format("s");
      setTimeout(() => timer(), 1000);
    };

    onMounted(() => {
      differ();
      timer();
    });

    return { state };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Itim&display=swap");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  font-family: "Itim", cursive;
  font-size: 20px;
}

.header {
  width: 100vw;
  padding: 1em;
  background-color: #fa8fab;
  color: #fff;
  text-align: center;
}

.container {
  width: 85vw;
  margin: auto;
  max-width: 800px;
}

.title {
  font-size: 3em;
}

.subtitle {
  color: #fdd7e4;
}

li {
  list-style: none;
}

.date {
  font-size: 5em;
  margin: 0.3em;
}

.date ul,
.time ul {
  display: flex;
  justify-content: center;
}

.date li,
.time li {
  margin: 0 0.5em;
  text-align: center;
}

.date span,
.time span {
  display: block;
  text-align: center;
}

.date .unit {
  font-size: 2rem;
}

.time .unit {
  font-size: 1rem;
}

.time {
  font-size: 1.5em;
}

@media screen and (max-width: 600px) {
  body {
    font-size: 13px;
  }
}
</style>
