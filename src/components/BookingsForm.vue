<template>
<section>
    <form class="booking-form" v-on:submit="addBooking" method="POST">
        <div>
            <label for="customer-name">Enter Guest Name:</label>
            <input type="text" name="customer-name" v-model="name" required>
        </div>
        <div>
            <label for="customer-email">Enter Guest E-mail:</label>
            <input type="email" name="customer-email" v-model="email" required>
        </div>
        <div>
            <label for="checked-in">Check-in: </label>
            <input type="checkbox" name="checked-in" v-model="checkedIn">
        </div>
        <input type="submit" value="Add Booking">
    </form>
</section>
</template>

<script>
import BookingService from '@/services/BookingService.js'
import { eventBus } from '@/main.js'


export default {
    name: "bookings-form",

    data() {
        return {
            name: "",
            email: "",
            checkedIn: false
        }
    },
    methods: {
        addBooking(event) {
            event.preventDefault()
            const booking = {
                name: this.name,
                email: this.email,
                checkedIn: this.checkedIn
            }
            BookingService.postBooking(booking)
            .then(res => eventBus.$emit('booking-added', res))
            .then(
                this.name = "",
                this.email = "",
                this.checkedIn = false
            )
        }
    }
}
</script>

<style>

</style>