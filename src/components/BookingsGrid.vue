<template>
    <div>
        <ul>
            <booking v-for="(booking, index) in bookings" :booking="booking" :key='index'></booking>  
        </ul>
    </div>
</template>

<script>
import Booking from '@/components/Booking.vue'
export default {
    name: "bookings-grid",
    props: ["bookings"],
    components: {
        'booking': Booking
    }
}
</script>

<style>
ul {
    display: flex;
    flex-flow: row wrap;
}
</style>