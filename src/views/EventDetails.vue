<template>
  <div v-if="event">
    <h5>{{ event.category }}</h5>
    <h2>{{ event.title }}</h2>
    <p>{{ event.description }}</p>
    <p>{{ event.organizer }}</p>
    <p>{{ id }} {{ typeof id }}</p>
    <p>{{ numba }} {{ typeof numba }}</p>
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'

export default {
  name: 'EventDetails',
  props: ['id', 'numba'],
  data() {
    return {
      event: null
    }
  },
  created() {
    EventService.getEvent(this.id)
      .then((response) => {
        this.event = response.data
      })
      .catch((error) => {
        console.log(error)
      })
  }
}
</script>

<style></style>
