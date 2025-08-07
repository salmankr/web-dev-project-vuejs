<script setup>
import EventCard from '@/components/EventCard.vue'
import { onMounted, ref } from 'vue'
import EventService from '@/services/EventService.js'

const events = ref(null)

onMounted( () => {
  // mock json server - this is set up adding a db.json file to a git repo
  // and configuring with my-json-server.typicode.com
  EventService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.log(error)
    })
})

</script>

<template>
  <h2>Events For Good</h2>
  <div class="events">
    <RouterLink to="/event/123">
      <EventCard v-for="event in events" :key="event.id" :event="event"/>
    </RouterLink>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
