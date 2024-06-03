<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { RouterLink, useRouter } from 'vue-router'
const router = useRouter()
import { Facebook, Twitter, Youtube } from 'lucide-vue-next'
import heroImage from '../assets/background1920.png'
const isMenuOpen = ref(false)
const lrn = ref('')
const password = ref('')
const loginError = ref(null)

async function login() {

  axios.post('/https://ndparang.info/api/v1/uri/login', {
        lrn: lrn.value,
        password: password.value
  })
  .then(function (response) {
    console.log(response);
    //     localStorage.setItem('access_token', response.data.accessToken)
    // localStorage.setItem('refresh_token', response.data.refreshToken)
    // router.push('/profile')
  })
  .catch(function (error) {
    console.log(error);
    loginError.value = error.response.data.error.message
  });

  try {
    const response = await axios.post(
      'https://ndparang.info/api/v1/uri/login',
      {
        lrn: lrn.value,
        password: password.value
      }
    )

  } catch (error) {
    
  }
}
</script>
<template>
  <div class="bg-gray-800">
    <nav class="bg-gray-900 fixed top-0 w-full z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-20">
          <img src="@/assets/ndparang_logo.png" class="h-14 mr-3" alt="logo" />
          <div class="flex-shrink-0">
            <a href="#" class="text-white font-semibold text-xl"
              >Notre Dame of Parang Inc.</a
            >
          </div>
          <!-- Mobile menu toggle -->
          <div class="flex md:hidden">
            <button
              @click="isMenuOpen = !isMenuOpen"
              class="text-gray-300 hover:text-white focus:outline-none focus:text-white"
              aria-label="Toggle menu"
            >
              <svg
                class="h-6 w-6"
                :class="{ hidden: isMenuOpen, block: !isMenuOpen }"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M4 6h16M4 12h16M4 18h16"
                />
              </svg>
              <svg
                class="h-6 w-6"
                :class="{ hidden: !isMenuOpen, block: isMenuOpen }"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M6 18L18 6M6 6l12 12"
                />
              </svg>
            </button>
          </div>
          <!-- Menu items -->
          <div class="hidden md:flex md:justify-center md:flex-grow">
            <div class="flex space-x-4">
              <a
                href="#"
                class="text-[#00923f] hover:text-green-600 px-3 py-2 rounded-md text-sm font-medium"
                >Home</a
              >
              <a
                href="https://alumni.ndparang.info"
                target="_blank"
                class="text-gray-300 hover:text-green-600 px-3 py-2 rounded-md text-sm font-medium"
                >Alumni</a
              >
              <a
                href="#"
                class="text-gray-300 hover:text-green-600 px-3 py-2 rounded-md text-sm font-medium"
                >About</a
              >
              <a
                href="#"
                class="text-gray-300 hover:text-green-600 px-3 py-2 rounded-md text-sm font-medium"
                >Contact us</a
              >
            </div>
          </div>
          <!-- Social media icons -->
          <div class="hidden md:flex items-center">
            <button
              type="button"
              class="inline-flex items-center font-medium justify-center px-1 py-1 mr-4 bg-white rounded-full text-sm text-gray-900 dark:text-white cursor-pointer hover:bg-gray-100 dark:hover:bg-gray-700 dark:hover:text-white"
            >
              <a href="https://www.facebook.com/ndparanginc/" target="_blank">
                <Facebook color="black" :size="24" />
              </a>
            </button>
            <button
              type="button"
              class="inline-flex items-center font-medium justify-center px-1 py-1 mr-4 bg-white rounded-full text-sm text-gray-900 dark:text-white cursor-pointer hover:bg-gray-100 dark:hover:bg-gray-700 dark:hover:text-white"
            >
              <a href="https://www.facebook.com/ndparanginc/" target="_blank">
                <Twitter color="black" :size="24" />
              </a>
            </button>
            <button
              type="button"
              class="inline-flex items-center font-medium justify-center px-1 py-1 bg-white rounded-full text-sm text-gray-900 dark:text-white cursor-pointer hover:bg-gray-100 dark:hover:bg-gray-700 dark:hover:text-white"
            >
              <a href="https://www.facebook.com/ndparanginc/" target="_blank">
                <Youtube color="black" :size="24" />
              </a>
            </button>
          </div>
        </div>
        <!-- Mobile menu -->
        <div
          class="md:hidden"
          :class="{ block: isMenuOpen, hidden: !isMenuOpen }"
        >
          <div
            class="md:hidden"
            :class="{ block: isMenuOpen, hidden: !isMenuOpen }"
          >
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
              <a
                href="#"
                class="text-[#00923f] hover:text-green-600 block px-3 py-2 rounded-md text-base font-medium"
                >Home</a
              >
              <a
                href="https://alumni.ndparang.info"
                class="text-gray-300 hover:text-green-600 block px-3 py-2 rounded-md text-base font-medium"
                >Alumni</a
              >
              <a
                href="#"
                class="text-gray-300 hover:text-green-600 block px-3 py-2 rounded-md text-base font-medium"
                >About</a
              >
              <a
                href="#"
                class="text-gray-300 hover:text-green-600 block px-3 py-2 rounded-md text-base font-medium"
                >Contact us</a
              >
            </div>
            <!-- Social media icons -->
            <div class="pt-4 pb-3 border-t border-gray-700">
              <div class="flex items-center px-5">
                <div class="flex-shrink-0">
                  <button
                    type="button"
                    class="inline-flex items-center font-medium justify-center px-1 py-1 mr-4 bg-white rounded-full text-sm text-gray-900 dark:text-white cursor-pointer hover:bg-gray-100 dark:hover:bg-gray-700 dark:hover:text-white"
                  >
                    <Facebook color="black" :size="24" />
                  </button>
                  <button
                    type="button"
                    class="inline-flex items-center font-medium justify-center px-1 py-1 mr-4 bg-white rounded-full text-sm text-gray-900 dark:text-white cursor-pointer hover:bg-gray-100 dark:hover:bg-gray-700 dark:hover:text-white"
                  >
                    <Twitter color="black" :size="24" />
                  </button>
                  <button
                    type="button"
                    class="inline-flex items-center font-medium justify-center px-1 py-1 bg-white rounded-full text-sm text-gray-900 dark:text-white cursor-pointer hover:bg-gray-100 dark:hover:bg-gray-700 dark:hover:text-white"
                  >
                    <Youtube color="black" :size="24" />
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <!-- Hero section -->
    <div class="relative">
      <!-- Background image -->
      <div
        class="h-screen md:h-screen bg-cover bg-center bg-no-repeat"
        :style="{ backgroundImage: `url(${heroImage})` }"
      ></div>
      <!-- Welcome message and login form -->
      <div
        class="absolute inset-0 flex flex-col justify-center items-center px-4 py-12 md:p-24 md:mt-60"
      >
        <div class="container mx-auto md:w-full flex flex-col md:flex-row">
          <!-- Welcome message -->
          <div
            class="w-full mt-52 md:mt-4 md:w-1/2 text-white md:text-left md:ml-40"
          >
            <h1
              class="text-3xl text-center mt-16 md:text-6xl md:text-start font-bold tracking-wider"
            >
              Enroll Anytime, Anywhere: Unleash Your Learning Journey!
            </h1>
            <p
              class="mt-5 text-lg text-gray-300 text-center md:text-start md:text-xl md:mt-10"
            >
              Welcome to effortless online enrollment! Join us from anywhere,
              anytime, and unlock your educational journey with ease.
            </p>
            <div
              class="flex place-content-center md:place-content-start mt-10 md:mt-10"
            >
              <router-link to="/register">
                <button
                  class="bg-[#00923f] hover:bg-green-600 text-white font-bold text-lg py-2 px-4 w-60 h-16 rounded-full"
                >
                  Pre-Enroll Now!
                </button>
              </router-link>
            </div>
          </div>
          <!-- Login form -->
          <div
            class="flex justify-center md:justify-end w-full md:w-1/2 mt-10 md:mt-0"
          >
            <div
              class="w-full bg-white rounded-lg shadow md:mt-0 md:mr-40 sm:max-w-md xl:p-0"
            >
              <div class="p-6 space-y-4 md:space-y-10 sm:p-8">
                <h1
                  class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl"
                >
                  Sign in to your account
                </h1>
                <form
                  @submit.prevent="submitForm"
                  class="space-y-4 md:space-y-6"
                >
                  <div>
                    <label
                      for="lrn"
                      class="block mb-2 text-sm font-medium text-gray-900"
                      >Your lrn</label
                    >
                    <input
                      v-model="lrn"
                      type="text"
                      name="lrn"
                      id="lrn"
                      class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5"
                      placeholder="ex.00-000-000-00"
                      required=""
                    />
                  </div>
                  <div>
                    <label
                      for="password"
                      class="block mb-2 text-sm font-medium text-gray-900"
                      >Password</label
                    >
                    <input
                      v-model="password"
                      type="password"
                      name="password"
                      id="password"
                      placeholder="••••••••"
                      class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5"
                      required=""
                    />
                  </div>
                  <div class="flex items-center justify-between">
                    <div class="flex items-start">
                      <div class="flex items-center h-5">
                        <input
                          id="remember"
                          aria-describedby="remember"
                          type="checkbox"
                          class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-primary-300"
                          required=""
                        />
                      </div>
                      <div class="ml-3 text-sm">
                        <label for="remember" class="text-gray-500"
                          >Remember me</label
                        >
                      </div>
                    </div>
                    <router-link to="/password_reset">
                      <button
                        class="text-sm font-medium text-primary-600 hover:underline hover:text-green-600"
                      >
                        Forgot password?
                      </button>
                    </router-link>
                  </div>
                  <p v-if="loginError" class="text-red-500 mt-1 mb-1 text-sm">
                    {{ loginError }}
                  </p>
                  <button
                    type="button"
                    @click="login"
                    class="w-full text-white bg-[#00923f] hover:bg-green-600 focus:ring-4 focus:outline-none focus:ring-green-500 font-medium rounded-lg text-sm px-5 py-2.5 text-center"
                  >
                    Sign in
                  </button>
                  <p class="text-sm font-light text-gray-500">
                    Don’t have an account yet?
                    <router-link
                      to="/register"
                      class="font-medium text-primary-600 hover:underline hover:text-green-700"
                    >
                      Sign up
                    </router-link>
                  </p>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
