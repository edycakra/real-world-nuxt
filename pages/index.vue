<template>
  <div>
    <h1>EVENTS</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'

export default {
  components: {
    EventCard
  },
  // asyncData({ $axios, error }) {
  //   return $axios
  //     .get('http://localhost:3000/events')
  //     .then((response) => {
  //       return {
  //         events: response.data
  //       }
  //     })
  //     .catch((e) => {
  //       error({
  //         statusCode: 503,
  //         message: `Unable to fetch. Please retry.`
  //       })
  //     })
  // },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: `Unable to fetch. Please retry.`
      })
    }
  },
  computed: mapState({
    events: (state) => state.events.events
  }),
  head() {
    // vue-meta properties
    return {
      title: 'Event Listing'
    }
  }
}
</script>

<style></style>
