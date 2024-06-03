<script setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import HomeView from './views/HomeView.vue'

const route = useRoute()
const router = useRouter()
// const isLoggedIn = computed(() => {
//   const token = localStorage.getItem('access_token')
//   return token !== null && token !== undefined
// })

// if (route.path !== '/register' && route.path !== '/register' && !isLoggedIn.value) {
//   router.push('/')
// }
</script>
<template>
  <router-view></router-view>
</template>
