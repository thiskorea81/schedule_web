<template>
    <div class="schedule">
      <h2>My Schedule</h2>
      <ul>
        <li v-for="event in events" :key="event.id">
          <span @click="editEvent(event)">{{ event.date }} {{ event.time }}: {{ event.title }}</span>
          <button @click="deleteEvent(event.id)">Delete</button>
        </li>
      </ul>
      <input v-model="newEventTitle" placeholder="Event Title" />
      <input v-model="newEventDate" type="date" />
      <input v-model="newEventTime" type="time" />
      <button @click="addEvent">Add Event</button>
      <button v-if="isEditing" @click="updateEvent">Update Event</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        events: JSON.parse(localStorage.getItem('events') || '[]'),
        newEventTitle: '',
        newEventDate: '',
        newEventTime: '',
        isEditing: false,
        currentEvent: null
      };
    },
    methods: {
      addEvent() {
        if (this.newEventTitle && this.newEventDate && this.newEventTime) {
          const newEvent = {
            id: Date.now(),
            title: this.newEventTitle,
            date: this.newEventDate,
            time: this.newEventTime
          };
          this.events.push(newEvent);
          this.saveEvents();
          this.resetForm();
          this.$emit('update-events', this.events);
        }
      },
      editEvent(event) {
        this.isEditing = true;
        this.currentEvent = event;
        this.newEventTitle = event.title;
        this.newEventDate = event.date;
        this.newEventTime = event.time;
      },
      updateEvent() {
        if (this.currentEvent) {
          this.currentEvent.title = this.newEventTitle;
          this.currentEvent.date = this.newEventDate;
          this.currentEvent.time = this.newEventTime;
          this.saveEvents();
          this.resetForm();
          this.$emit('update-events', this.events);
        }
      },
      deleteEvent(id) {
        this.events = this.events.filter(event => event.id !== id);
        this.saveEvents();
        this.$emit('update-events', this.events);
      },
      saveEvents() {
        localStorage.setItem('events', JSON.stringify(this.events));
      },
      resetForm() {
        this.newEventTitle = '';
        this.newEventDate = '';
        this.newEventTime = '';
        this.isEditing = false;
        this.currentEvent = null;
      }
    }
  };
  </script>
  
  
  <style scoped>
  .schedule {
    max-width: 400px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  input {
    display: block;
    width: 100%;
    padding: 8px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  button {
    padding: 10px 15px;
    background-color: #42b983;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #38a373;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin: 10px 0;
  }
  span {
    cursor: pointer;
  }
  </style>
  