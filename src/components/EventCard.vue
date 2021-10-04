<template>
  <router-link
    class="event-link"
    :to="{ name: 'EventDetails', params: { id: event.id } }"
  >
    <div class="event-card">
      <h4>{{ event.title }}</h4>
      <p>{{ event.description }}</p>
    </div>
  </router-link>
</template>

<script>
export default {
  props: {
    event: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.event-card {
  margin: 0 0 18px 0;
  border: 1px solid black;
  padding: 16px;
  width: 256px;
  cursor: pointer;
}

.event-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 128, 128, 0.9);
}

.event-link {
  color: teal;
  text-decoration: none;
}
</style>
