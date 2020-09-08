<template>
  <div>
    <h1>Events</h1>
    <EventCard 
      v-for="(event, index ) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '../components/eventCard.vue'
export default {
  components: {
    EventCard
  },
  computed: mapState({
    events: state => state.event.events
  }),
  head() {
    return {
      title: 'Event Listing '
    }
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('event/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events, try again'
      })
    }
  }
}
</script>
