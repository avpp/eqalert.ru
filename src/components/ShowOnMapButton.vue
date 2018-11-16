<template>
  <div>
    <a href="#" @click.prevent="showModal = true">
      <span v-if="!$root.onMobile">Показать на карте</span>
      <i class="fa fa-lg fa-map align-middle" aria-hidden="true" />
    </a>
    <Modal v-if="showModal" @close="showModal = false" width="wide">
      <h3 slot="header">На карте</h3>
      <div slot="body">
        <EventsMap :events="events" />
      </div>
      <span slot="footer"></span>
    </Modal>
  </div>
</template>

<script>
import Modal from '@/components/Modal.vue'
import EventsMap from '@/components/maps/Events.vue'

export default {
  components: { Modal, EventsMap },
  props: ['events'],
  data() {
    return {
      showModal: false
    }
  }
}
</script>
<style lang="scss" scoped>
  @import '~scss/global';
  .fa {
    color: $color-orange;
    padding-left: 1%;
  }
</style>

