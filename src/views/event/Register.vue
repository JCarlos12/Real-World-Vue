<script setup>
import { useRouter } from 'vue-router'
import { defineProps, inject } from 'vue'

const { event } = defineProps(['event'])
const router = useRouter()
const GStore = inject('GStore')
const register = () => {
  //If registration API call is successful
  GStore.flashMessage = 'You are successfully registered for ' + event.title
  setTimeout(() => {
    GStore.flashMessage = ''
  }, 3000)
  router.push({
    name: 'EventDetails',
  })
}
</script>

<template>
  <p>Register for the Event</p>
  <button @click="register">Register Me!</button>
</template>
