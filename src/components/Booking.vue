<template>
    <div id=bookingcard>

        <h3>{{ booking.name }}</h3>
        <p>{{ booking.email }}</p>
        <p v-if=booking.checkedIn>Checked in? &#9989; </p>
        <p v-if=!booking.checkedIn>Checked in? &#10060; </p>


        <button type="button" v-on:click="deleteBooking">Booking Begone</button>
    </div>
</template>

<script>
import { eventBus } from '@/main.js'
import BookingService from '@/services/BookingService.js'

export default {
    name: 'booking',
    props: ['booking'],

    methods: {
        deleteBooking() {
            BookingService.deleteBooking(this.booking._id)
            .then(() => eventBus.$emit('booking-deleted', this.booking._id))
        },    

        updateBooking() {
            BookingService.updateBooking(this.booking._id)
            .then(() => eventBus.$emit('booking-updated', this.booking._id))
        }
    }
}
</script>

<style>
#bookingcard {
    background-color: fuchsia;
    border: 10px groove yellow;
    padding: 10px;
    margin: 20px;
    min-width: 200px;
}
</style>