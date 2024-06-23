<template>
  <div class="calendar">
    <div class="header">
      <button @click="prevMonth">Prev</button>
      <h2>{{ monthNames[currentMonth] }} {{ currentYear }}</h2>
      <button @click="nextMonth">Next</button>
    </div>
    <div class="weekdays">
      <div v-for="day in weekDays" :key="day">{{ day }}</div>
    </div>
    <div class="days">
      <div
        v-for="day in daysInMonth"
        :key="day.date ? day.date.toDateString() : day.index"
        :class="{'today': isToday(day.date), 'has-event': hasEvent(day.date)}"
      >
        <span v-if="day.date">{{ day.date.getDate() }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    events: Array
  },
  data() {
    return {
      currentDate: new Date(),
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      weekDays: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
      monthNames: [
        'January', 'February', 'March', 'April', 'May', 'June',
        'July', 'August', 'September', 'October', 'November', 'December'
      ]
    };
  },
  computed: {
    daysInMonth() {
      const days = [];
      const firstDay = new Date(this.currentYear, this.currentMonth, 1).getDay();
      const lastDate = new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
      for (let i = 0; i < firstDay; i++) {
        days.push({ date: null, index: `empty-${i}` });
      }
      for (let date = 1; date <= lastDate; date++) {
        days.push({ date: new Date(this.currentYear, this.currentMonth, date) });
      }
      return days;
    }
  },
  methods: {
    prevMonth() {
      if (this.currentMonth === 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    nextMonth() {
      if (this.currentMonth === 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    isToday(date) {
      if (!date) return false;
      const today = new Date();
      return date.getDate() === today.getDate() &&
             date.getMonth() === today.getMonth() &&
             date.getFullYear() === today.getFullYear();
    },
    hasEvent(date) {
      if (!date) return false;
      return this.events.some(event => {
        const eventDate = new Date(event.date);
        return eventDate.getDate() === date.getDate() &&
               eventDate.getMonth() === date.getMonth() &&
               eventDate.getFullYear() === date.getFullYear();
      });
    }
  }
};
</script>

<style scoped>
.calendar {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.weekdays {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}
.days {
  display: flex;
  flex-wrap: wrap;
}
.days div {
  width: calc(100% / 7);
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;
}
.today {
  background-color: #42b983;
  color: white;
  border-radius: 50%;
}
.has-event {
  background-color: purple;
  color: white;
  border-radius: 50%;
}
</style>
