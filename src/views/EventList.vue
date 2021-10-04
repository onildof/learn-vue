<template>
  <h1>Assorted Cards</h1>
  <div class="events">
    <event-card
      v-for="event in events"
      :key="event"
      :event="event"
    ></event-card>
    <div class="pagination">
      <router-link
        id="page-prev"
        :to="{ name: 'EventList', query: { page: page - 1 } }"
        rel="prev"
        v-if="page != 1"
        >&lt; Prev</router-link
      >
      <router-link
        v-for="pageNumber in Math.ceil(totalEventCount / 2)"
        :key="pageNumber"
        :to="{ name: 'EventList', query: { page: pageNumber } }"
        >{{ pageNumber }}</router-link
      >
      <router-link
        id="page-next"
        :to="{ name: 'EventList', query: { page: page + 1 } }"
        rel="next"
        v-if="hazNextPage"
        >Next &gt;</router-link
      >
    </div>
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'
import { watchEffect } from 'vue'

export default {
  name: 'EventList',
  components: {
    EventCard
  },
  props: ['page'],
  data() {
    return {
      events: null,
      totalEventCount: 0
    }
  },
  computed: {
    hazNextPage() {
      return this.page * 2 < this.totalEventCount
    }
  },
  created() {
    watchEffect(() => {
      this.events = null
      EventService.getEvents(2, this.page)
        .then((response) => {
          this.events = response.data
          this.totalEventCount = response.headers['x-total-count']
        })
        .catch((error) => console.log(error))
    })
  }
}
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pagination {
  display: flex;
  justify-content: space-between;
  width: 288px;
}

.pagination a {
  flex: 1;
  color: teal;
  text-decoration: none;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>
