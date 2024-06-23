<template>
    <div>
      <Calendar :events="events" />
      <Schedule @update-events="updateEvents" />
    </div>
  </template>
  
  <script>
  import Calendar from './Calendar.vue';
  import Schedule from './Schedule.vue';
  
  export default {
    name: 'SideBar',
    components: {
      Calendar,
      Schedule
    },
    data() {
      return {
        events: JSON.parse(localStorage.getItem('events') || '[]')
      };
    },
    methods: {
      updateEvents(events) {
        this.events = events;
      }
    }
  };
  </script>
  