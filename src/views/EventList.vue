<script setup>
import EventCard from "@/components/EventCard.vue";
import EventService from "@/services/EventService.js";
import { onMounted, ref, computed } from "vue";

const propd = defineProps(['page'])
const events = ref("");
const page = computed(() => props.page)

onMounted(() => {
  EventService.getEvents(2, page.value)
    .then((response) => {
      events.value = response.data;
    })
    .catch((error) => {
      console.log(error);
    });
});
</script>

<template>
  <h1>Events for Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
