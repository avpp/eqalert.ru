<template>
  <GeneralEventsMap :eventsProvider="eventsProvider"></GeneralEventsMap>
</template>

<script>
import GeneralEventsMap from '@/components/maps/GeneralEvents.vue'
export default {
  components: { GeneralEventsMap },
  computed: {
    eventsProvider: function() {
      return {
        fillEvents: (eventWaiter) => {
          this.$http.get(this.$root.$options.settings.api.endpointEvents, {
            params: {
              datetime_min: this.$moment().subtract(3, 'months').format('YYYY-MM-DD HH:mm:ss'),
              limit: 500
            }
          })
            .then(response => { eventWaiter.addEvents(response.data.data) })
            .catch(error => { console.log(error) })
        }
      }
    }
  }
}
</script>
