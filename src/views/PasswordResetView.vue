<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'
const router = useRouter()
const resetError = ref(null)
const errors = ref({})
const lrn = ref('')
const code = ref('')
const state = ref('reset')

const restrictLRN = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 12)
  lrn.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 12) {
    event.target.blur()
  }
}

async function reset_password() {
  errors.value = {}
  if (!lrn.value) {
    errors.value.lrn = 'lrn is required'
  } else {
    try {
      const response = await axios.patch(
        'https://ndparang.info/api/v1/uri/reset_password',
        {
          lrn: lrn.value
        }
      )
      if (response.status === 202) {
        state.value = 'confirm'
      }
    } catch (error) {
      resetError.value = error.response.data.error.message
    }
  }
}

async function confirm_code() {
  errors.value = {}
  if (!code.value) {
    errors.value.code = 'code is required'
  } else {
    try {
      const response = await axios.post(
        'https://ndparang.info/api/v1/uri/confirm_code',
        {
          code: code.value
        }
      )
      localStorage.setItem('access_token', response.data.accessToken)
      localStorage.setItem('refresh_token', response.data.refreshToken)
      router.push('/profile')
    } catch (error) {
      resetError.value = error.response.data.error.message
    }
  }
}
</script>
<template>
  <div
    class="sm:flex sm:justify-center sm:items-center min-h-screen bg-dots-darker bg-center bg-gray-900 dark:bg-dots-lighter dark:bg-gray-900 selection:bg-red-500 selection:text-white"
  >
    <div
      class="flex flex-col max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-screen justify-center items-center"
    >
      <div class="flex items-center justify-center h-20 mt-10 md:mt-0">
        <div class="flex-none w-14 h-14 mr-2">
          <img src="@/assets/ndparang_logo.png" class="h-14" alt="logo" />
        </div>
        <div class="flex items-center justify-center w-fit h-14">
          <a href="#" class="text-white font-semibold text-xl"
            >Notre Dame of Parang Inc.</a
          >
        </div>
      </div>

      <div v-if="state === 'reset'" class="flex flex-col items-center mt-8">
        <h1 class="text-slate-300 text-base">Reset your password</h1>
        <p class="text-slate-100 text-center text-sm mt-2 w-96 px-5">
          Enter the lrn number you used when you joined and we'll send you a
          code to your email to reset your password.
        </p>
      </div>
      <div v-if="state === 'reset'" class="flex flex-col w-80 md:w-96 mt-8">
        <p v-if="resetError" class="text-red-500 mt-1 mb-1 text-sm">
          {{ resetError }}
        </p>
        <label
          for="lrn"
          class="font-normal text-base mb-1 text-slate-300 block mt-5"
          >LRN Number</label
        >
        <input
          v-model="lrn"
          type="lrn"
          :class="{ 'border border-red-500': errors.lrn }"
          @input="restrictLRN"
          maxlength="255"
          class="px-3 py-3 bg-slate-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
          placeholder=""
        />
        <button
          type="button"
          @click="reset_password"
          class="w-full text-white bg-[#00923f] hover:bg-green-600 focus:ring-4 focus:outline-none focus:ring-green-600 font-medium rounded-lg text-sm px-5 py-2.5 mt-8 text-center"
        >
          Reset your password
        </button>
      </div>

      <div v-if="state === 'confirm'" class="flex flex-col w-80 md:w-96 mt-8">
        <h2 class="text-green-500 text-base text-center">
          A reset code has been sent to your email.
        </h2>
        <p v-if="resetError" class="text-red-500 text-sm mt-5">
          {{ resetError }}
        </p>
        <label
          for="lrn"
          class="font-normal text-base mb-1 text-slate-300 block mt-8"
          >Reset Code</label
        >
        <input
          v-model="code"
          type="code"
          :class="{ 'border border-red-500': errors.code }"
          class="px-3 py-3 bg-slate-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
          placeholder=""
        />
        <button
          type="button"
          @click="confirm_code"
          class="w-full text-white bg-[#00923f] hover:bg-green-600 focus:ring-4 focus:outline-none focus:ring-green-600 font-medium rounded-lg text-sm px-5 py-2.5 mt-8 text-center"
        >
          Confirm Code
        </button>
      </div>

      <div class="flex flex-row mt-8">
        <p class="text-sm font-light text-gray-500">
          <router-link to="/">
            <a
              href="#"
              class="font-medium text-sm text-primary-600 hover:underline"
              >Back to home</a
            >
          </router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<style>
.bg-dots-darker {
  background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(0,0,0,0.07)'/%3E%3C/svg%3E");
}

@media (prefers-color-scheme: dark) {
  .dark\:bg-dots-lighter {
    background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(255,255,255,0.07)'/%3E%3C/svg%3E");
  }
}
</style>
