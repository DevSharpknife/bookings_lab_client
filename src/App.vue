<template>
<section>
  <div id="app">
    <header>
      <h1>THIS IS THE APP PART</h1>
    </header>
      <main>
        <bookings-form></bookings-form>
        <bookings-grid :bookings="bookings"></bookings-grid>
      </main>
    <footer>
      <p>Booking System Footer</p>
    </footer>
  </div>
</section>  
</template>

<script>
import BookingService from './services/BookingService.js'
import BookingsForm from './components/BookingsForm.vue'
import BookingsGrid from './components/BookingsGrid.vue'
import { eventBus } from '@/main.js';
export default {
  name: 'app',
  components: {
    'bookings-form': BookingsForm,
    'bookings-grid': BookingsGrid
  },
  
  data() {
    return {
      bookings: []
    }
  },
  mounted() {
    this.fetchBookings();
    
    eventBus.$on('booking-added', (booking) => {
        this.bookings.push(booking)
    });

    eventBus.$on('booking-deleted', (id) => {
      let index = this.bookings.findIndex((booking) => booking._id === id) 
      this.bookings.splice(index, 1)
    });  
  },
  methods: {
    fetchBookings() {
      BookingService.getBookings()
        .then(bookings => this.bookings = bookings);
    }
  }
}
</script>

<style>
body {
    margin:0;
}
#app {
    display: grid;
    grid-template-rows: 100px auto 100px;
    max-height: 100vh;
    min-height: 100vh;
    grid-template-areas:
    "header"
    "main"
    "footer";
}
header {
    grid-area: header;
    background-color: rgb(72, 0, 94);
    padding:10px;
    color: white;
}
footer {
    grid-area: footer;
    background-color: rgb(72, 0, 94);
    padding:10px;
    color: white;
}
main {
    grid-area: main;
    padding:10px;
}
</style>