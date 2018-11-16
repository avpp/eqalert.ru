<template>
  <GeneralEventsMap :eventsProvider="eventsProvider"></GeneralEventsMap>
</template>

<script>
import GeneralEventsMap from '@/components/maps/GeneralEvents.vue'
export default {
  props: ['events'],
  components: { GeneralEventsMap },
  computed: {
    eventsProvider: function() {
      return {
        fillEvents: (eventWaiter) => {
          eventWaiter.addEvents(this.events)
        }
      }
    }
  }
}
</script>
