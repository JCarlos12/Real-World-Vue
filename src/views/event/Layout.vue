<script setup>
import { useRouter } from 'vue-router'
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'
const router = useRouter()
const event = ref(null)
const props = defineProps({
  id: {
    required: true,
  },
})
onMounted(() => {
  EventService.getEvent(props.id)
    .then((response) => {
      console.log(response)
      event.value = response.data
    })
    .catch((error) => {
      if (error.response && error.response.status === 404) {
        router.push({
          name: '404Resource',
          params: { resource: 'event' },
        })
      } else {
        router.push({ name: 'NetworkError' })
      }
    })
})
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'EventDetails' }">Details</router-link>
      |
      <router-link :to="{ name: 'EventRegister' }">Register</router-link>
      |
      <router-link :to="{ name: 'EventEdit' }">Edit</router-link>
    </div>
    <router-view :event="event" />
  </div>
</template>
