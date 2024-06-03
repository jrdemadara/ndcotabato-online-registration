<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'
const router = useRouter()
import {
  UserCircle,
  Users,
  RedoDot,
  School2,
  Shield,
  SquareEqual,
  CheckCircle2,
  XCircle,
  LogOut
} from 'lucide-vue-next'
import flatPickr from 'vue-flatpickr-component'
import 'flatpickr/dist/flatpickr.css'

const access_token = localStorage.getItem('access_token')
const refresh_token = localStorage.getItem('refresh_token')

const currentTab = ref(1)
const isEdit = ref('')

const isLoading = ref(false)
const isError = ref(false)

const lastname = ref('')
const firstname = ref('')
const middlename = ref('')
const extension = ref('')
const birthdate = ref('')
const origin = ref('')
const puroksitio = ref('')
const fathersname = ref('')
const foccupation = ref('')
const fmonincome = ref('')
const mothersname = ref('')
const moccupation = ref('')
const mmonincome = ref('')
const parentscontact = ref('')
const parentsaddress = ref('')
const noofsiblings = ref('')
const guardiansname = ref('')
const gcontact = ref('')
const gaddress = ref('')
const schoollast = ref('')
const schooladdress = ref('')
const yeargraduated = ref('')
const average = ref('')
const lrnno = ref('')
const emailadd = ref('')
const contactno = ref('')
const password = ref('')

const province = ref('')
const municipality = ref('')
const barangay = ref('')
const diaserial = ref('')
const relserial = ref('')
const gender = ref('')
const civilstatus = ref('')

const h2_lastname = ref('')
const h2_firstname = ref('')
const h2_middlename = ref('')
const h2_extension = ref('')
const h2_birthdate = ref('')
const h2_gender = ref('')
const h2_civilstatus = ref('')
const h2_religion = ref('')
const h2_dialect = ref('')
const h2_origin = ref('')
const h2_province = ref('')
const h2_municipality = ref('')
const h2_barangay = ref('')
const h2_puroksitio = ref('')
const h2_fathersname = ref('')
const h2_fathers_occupation = ref('')
const h2_fathers_income = ref('')
const h2_mothersname = ref('')
const h2_mothers_occupation = ref('')
const h2_mothers_income = ref('')
const h2_parents_contact = ref('')
const h2_parents_address = ref('')
const h2_noofsiblings = ref('')
const h2_guardiansname = ref('')
const h2_guardians_contact = ref('')
const h2_guardians_address = ref('')
const h2_schoollast = ref('')
const h2_schooladdress = ref('')
const h2_yeargraduated = ref('')
const h2_average = ref('')
const h2_lrn = ref('')
const h2_emailadd = ref('')
const h2_contactno = ref('')
const h2_password = ref('')

// Options Data
const provinceOptions = ref([])
const religionOptions = ref([])
const dialectOptions = ref([])
const municipalityOptions = ref([])
const barangayOptions = ref([])

// Populate Profile
onMounted(async () => {
  isLoading.value = true
  axios
    .post('https://ndcotabato.info/api/v1/uri/profile', {
      headers: {
        Authorization: `Bearer ${access_token}`,
        'Content-Type': 'application/json'
      }
    })
    .then(function (response) {
      //       AND addressprovinces.provCode = :province
      // AND addresscitymuns.citymunCode = :municipality
      // AND addressbrgys.brgyCode = :barangay
      // AND dialects.diaserial = :dialect
      // AND religions.relserial = :religion;
      h2_lastname.value = response.data.profile[0].lastname
      h2_firstname.value = response.data.profile[0].firstname
      h2_middlename.value = response.data.profile[0].middlename
      h2_extension.value = response.data.profile[0].extension
      h2_birthdate.value = response.data.profile[0].birthdate
      h2_gender.value = response.data.profile[0].gender
      h2_civilstatus.value = response.data.profile[0].civilstatus
      h2_religion.value = response.data.profile[0].relname
      h2_dialect.value = response.data.profile[0].dianame
      h2_origin.value = response.data.profile[0].origin
      h2_province.value = response.data.profile[0].provDesc
      h2_municipality.value = response.data.profile[0].citymunDesc
      h2_barangay.value = response.data.profile[0].brgyDesc
      h2_puroksitio.value = response.data.profile[0].puroksitio
      h2_fathersname.value = response.data.profile[0].fathersname
      h2_fathers_occupation.value = response.data.profile[0].foccupation
      h2_fathers_income.value = response.data.profile[0].fmonincome
      h2_mothersname.value = response.data.profile[0].mothersname
      h2_mothers_occupation.value = response.data.profile[0].moccupation
      h2_mothers_income.value = response.data.profile[0].mmonincome
      h2_parents_contact.value = response.data.profile[0].parentscontact
      h2_parents_address.value = response.data.profile[0].parentsaddress
      h2_noofsiblings.value = response.data.profile[0].noofsiblings
      h2_guardiansname.value = response.data.profile[0].guardiansname
      h2_guardians_contact.value = response.data.profile[0].gcontact
      h2_guardians_address.value = response.data.profile[0].gaddress
      h2_schoollast.value = response.data.profile[0].schoollast
      h2_schooladdress.value = response.data.profile[0].schooladdress
      h2_yeargraduated.value = response.data.profile[0].yeargraduated
      h2_average.value = response.data.profile[0].average
      h2_lrn.value = response.data.profile[0].lrnno
      h2_emailadd.value = response.data.profile[0].emailadd
      h2_contactno.value = response.data.profile[0].contactno
      h2_password.value = response.data.profile[0].password

      lastname.value = response.data.profile[0].lastname
      firstname.value = response.data.profile[0].firstname
      middlename.value = response.data.profile[0].middlename
      extension.value = response.data.profile[0].extension
      //birthdate.value = response.data.profile[0].birthdate
      origin.value = response.data.profile[0].origin
      puroksitio.value = response.data.profile[0].puroksitio
      fathersname.value = response.data.profile[0].fathersname
      foccupation.value = response.data.profile[0].foccupation
      fmonincome.value = response.data.profile[0].fmonincome
      mothersname.value = response.data.profile[0].mothersname
      moccupation.value = response.data.profile[0].moccupation
      mmonincome.value = response.data.profile[0].mmonincome
      parentscontact.value = response.data.profile[0].parentscontact
      parentsaddress.value = response.data.profile[0].parentsaddress
      noofsiblings.value = response.data.profile[0].noofsiblings
      guardiansname.value = response.data.profile[0].guardiansname
      gcontact.value = response.data.profile[0].gcontact
      gaddress.value = response.data.profile[0].gaddress
      schoollast.value = response.data.profile[0].schoollast
      schooladdress.value = response.data.profile[0].schooladdress
      yeargraduated.value = response.data.profile[0].yeargraduated
      average.value = response.data.profile[0].average
      lrnno.value = response.data.profile[0].lrnno
      emailadd.value = response.data.profile[0].emailadd
      contactno.value = response.data.profile[0].contactno
      isLoading.value = false
      isError.value = false
    })
    .catch(function (error) {
      console.log(error)
      isLoading.value = false
      isError.value = true
    })

  try {
    const response = await axios.get(
      'https://ndcotabato.info/api/v1/uri/province',
      {
        headers: {
          'Content-Type': 'application/json'
        }
      }
    )
    const provinceData = await response.data.provinces
    const religionData = await response.data.religions
    const dialectData = await response.data.dialects
    religionOptions.value = religionData
    dialectOptions.value = dialectData
    provinceOptions.value = provinceData
  } catch (error) {
    console.error(error)
  }
})

// Populate Municipality
async function getMunicipality() {
  try {
    const response = await axios.post(
      'https://ndcotabato.info/api/v1/uri/municipality',
      {
        province: province.value,
        headers: {
          'Content-Type': 'application/json'
        }
      }
    )
    const municipalityData = await response.data.municipalities
    municipalityOptions.value = municipalityData
  } catch (error) {
    console.error(error)
  }
}

// Populate Barangay
async function getBarangay() {
  try {
    const response = await axios.post(
      'https://ndcotabato.info/api/v1/uri/barangay',
      {
        municipality: municipality.value,
        headers: {
          'Content-Type': 'application/json'
        }
      }
    )
    const barangayData = await response.data.barangays
    barangayOptions.value = barangayData
  } catch (error) {
    console.error(error)
  }
}

// Patch
async function patch(data) {
  try {
    const response = await axios.patch(
      'https://ndcotabato.info/api/v1/uri/profile',
      {
        field: isEdit.value,
        data: data,
        headers: {
          Authorization: `Bearer ${access_token}`,
          'Content-Type': 'application/json'
        }
      }
    )
    if (response.status === 200) {
      isEdit.value = ''
    }
  } catch (error) {
    console.error(error)
  }
}

async function patchPassword(data) {
  try {
    const response = await axios.patch(
      'https://ndcotabato.info/api/v1/uri/resetpassword',
      {
        password: data,
        headers: {
          Authorization: `Bearer ${access_token}`,
          'Content-Type': 'application/json'
        }
      }
    )
    if (response.status === 200) {
      isEdit.value = ''
    }
  } catch (error) {
    console.error(error)
  }
}

async function patchAddress(province, municipality, barangay, purok) {
  try {
    const response = await axios.patch(
      'https://ndcotabato.info/api/v1/uri/updateaddress',
      {
        province: province,
        municipality: municipality,
        barangay: barangay,
        purok: purok,
        headers: {
          Authorization: `Bearer ${access_token}`,
          'Content-Type': 'application/json'
        }
      }
    )
    if (response.status === 200) {
      isEdit.value = ''
    }
  } catch (error) {
    console.error(error)
  }
}

//Logout
async function logout() {
  try {
    const response = await axios.delete(
      'https://ndcotabato.info/api/v1/uri/logout',
      {
        headers: {
          Authorization: `Bearer ${refresh_token}`,
          'Content-Type': 'application/json'
        }
      }
    )
    if (response.status === 204) {
      localStorage.removeItem('access_token')
      localStorage.removeItem('refresh_token')
      router.push('/')
    }
  } catch (error) {
    console.error(error)
  }
}
</script>
<style>
.tab-button:hover span,
.tab-button:hover svg {
  color: white;
}

.tab-button:hover i {
  color: white;
}
</style>
<template>
  <div class="relative bg-white">
    <div
      v-if="isLoading"
      class="fixed inset-0 flex items-center justify-center bg-white bg-opacity-5 backdrop-blur-sm"
    >
      <div
        class="w-16 h-16 border-4 border-[#1C1AAB] border-dashed rounded-full animate-spin spinner"
      ></div>
    </div>

    <div
      v-if="isError"
      class="fixed inset-0 flex items-center justify-center bg-white bg-opacity-5 backdrop-blur-sm"
    >
      <h2 class="font-semibold text-red-500 text-lg text-center">
        Something went wrong with the server <br />
        Please try to reload.
      </h2>
    </div>

    <nav class="bg-gray-900 fixed top-0 w-full z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center md:justify-center h-20">
          <div class="flex-none w-14 h-14 mr-2">
            <img src="@/assets/logo.png" class="h-14" alt="logo" />
          </div>
          <div class="flex items-center w-screen h-14">
            <a href="#" class="text-white font-semibold text-xl"
              >Notre Dame of Cotabato</a
            >
          </div>
          <div class="flex justify-end w-fit h-14">
            <div class="flex items-center">
              <div class="hidden md:block lg:block flex justify-end w-56">
                <h2 class="text-white">
                  Hello,
                  <span class="text-[#1C1AAB] normal-case"
                    >{{ firstname }}!</span
                  >
                </h2>
              </div>
              <button
                @click="logout()"
                class="md:block lg:block flex items-center place-content-center bg-transparent text-white hover:text-red-500 mx-3"
              >
                <LogOut class="w-6 h-6" />
              </button>
              <img
                class="w-16 hidden md:block lg:block"
                src="@/assets/profile.svg"
                alt="profile"
              />
            </div>
          </div>
        </div>
      </div>
    </nav>
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-24 md:mt-32">
      <div class="flex flex-col">
        <div v-show="currentTab === 1">
          <h2 class="text-2xl font-bold">Profile</h2>
          <p class="text-slate-500 md:mt-2">
            View or update your profile settings
          </p>
        </div>
        <div v-show="currentTab === 2">
          <h2 class="text-2xl font-bold">Grades</h2>
          <p class="text-slate-500 md:mt-2">View or update your grades</p>
        </div>
        <div v-show="currentTab === 3">
          <h2 class="text-2xl font-bold">Parents/Guardians</h2>
          <p class="text-slate-500 md:mt-2">
            View or update your parent/guardians information
          </p>
        </div>
        <div v-show="currentTab === 4">
          <h2 class="text-2xl font-bold">Previous School</h2>
          <p class="text-slate-500 md:mt-2">
            View or update your previous school
          </p>
        </div>
        <div v-show="currentTab === 5">
          <h2 class="text-2xl font-bold">Security</h2>
          <p class="text-slate-500 md:mt-2">
            View or update your account security
          </p>
        </div>
      </div>
      <div class="container mx-auto mt-5 md:mt-10">
        <div class="border border-gray-200 rounded">
          <div class="flex">
            <button
              :class="{
                'bg-[#1C1AAB]': currentTab === 1,
                'bg-gray-200': currentTab != 1
              }"
              @click="currentTab = 1"
              class="flex flex-grow items-center justify-center px-4 py-2 md:py-5 hover:bg-blue-600 rounded-tl tab-button"
            >
              <i>
                <UserCircle
                  :class="{
                    'text-white': currentTab === 1,
                    'text-slate-500': currentTab != 1
                  }"
                  class="mr-0 md:mr-2"
                />
              </i>
              <span
                :class="{
                  'text-white': currentTab === 1,
                  'text-slate-500': currentTab != 1
                }"
                class="hidden md:block"
                >Profile</span
              >
            </button>

            <button
              :class="{
                'bg-[#1C1AAB]': currentTab === 3,
                'bg-gray-200': currentTab != 3
              }"
              @click="currentTab = 3"
              class="flex flex-grow items-center justify-center px-4 py-2 md:py-5 hover:bg-blue-600 tab-button"
            >
              <i>
                <Users
                  :class="{
                    'text-white': currentTab === 3,
                    'text-slate-500': currentTab != 3
                  }"
                  class="mr-0 md:mr-2"
                />
              </i>
              <span
                :class="{
                  'text-white': currentTab === 3,
                  'text-slate-500': currentTab != 3
                }"
                class="hidden md:block"
                >Parents/Guardians</span
              >
            </button>

            <button
              :class="{
                'bg-[#1C1AAB]': currentTab === 4,
                'bg-gray-200': currentTab != 4
              }"
              @click="currentTab = 4"
              class="flex flex-grow items-center justify-center px-4 py-4 md:py-5 hover:bg-blue-600 tab-button"
            >
              <i>
                <School2
                  :class="{
                    'text-white': currentTab === 4,
                    'text-slate-500': currentTab != 4
                  }"
                  class="mr-0 md:mr-2"
                />
              </i>
              <span
                :class="{
                  'text-white': currentTab === 4,
                  'text-slate-500': currentTab != 4
                }"
                class="hidden md:block"
                >Previous School</span
              >
            </button>

            <button
              :class="{
                'bg-[#1C1AAB]': currentTab === 2,
                'bg-gray-200': currentTab != 2
              }"
              @click="currentTab = 2"
              class="flex flex-grow items-center justify-center px-4 py-2 md:py-5 hover:bg-blue-600 tab-button"
            >
              <i>
                <SquareEqual
                  :class="{
                    'text-white': currentTab === 2,
                    'text-slate-500': currentTab != 2
                  }"
                  class="mr-0 md:mr-2"
                />
              </i>
              <span
                :class="{
                  'text-white': currentTab === 2,
                  'text-slate-500': currentTab != 2
                }"
                class="hidden md:block"
                >Grades</span
              >
            </button>

            <button
              :class="{
                'bg-[#1C1AAB]': currentTab === 5,
                'bg-gray-200': currentTab != 5
              }"
              @click="currentTab = 5"
              class="flex flex-grow items-center justify-center px-4 py-4 md:py-5 hover:bg-blue-600 tab-button"
            >
              <i>
                <Shield
                  :class="{
                    'text-white': currentTab === 5,
                    'text-slate-500': currentTab != 5
                  }"
                  class="mr-0 md:mr-2"
                />
              </i>
              <span
                :class="{
                  'text-white': currentTab === 5,
                  'text-slate-500': currentTab != 5
                }"
                class="hidden md:block"
                >Security</span
              >
            </button>
          </div>
          <div class="p-4">
            <div v-show="currentTab === 1">
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Lastname</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_lastname }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'lastname'">
                    <button
                      @click="isEdit = 'lastname'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'lastname'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="lastname"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(lastname)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Firstname</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_firstname }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'firstname'">
                    <button
                      @click="isEdit = 'firstname'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'firstname'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="firstname"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(firstname)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Middlename</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_middlename }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'middlename'">
                    <button
                      @click="isEdit = 'middlename'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'middlename'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="middlename"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(middlename)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Extension</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_extension }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'extension'">
                    <button
                      @click="isEdit = 'extension'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'extension'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="extension"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(extension)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Birthdate</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_birthdate }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'birthdate'">
                    <button
                      @click="isEdit = 'birthdate'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'birthdate'">
                    <div class="flex">
                      <flat-pickr
                        v-model="birthdate"
                        class="datepicker border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Select birthdate"
                        name="date"
                      />
                      <button
                        @click="patch(birthdate)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Gender</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_gender }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'gender'">
                    <button
                      @click="isEdit = 'gender'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'gender'">
                    <div class="flex">
                      <select
                        v-model="gender"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                      >
                        <option value="" selected disabled hidden>
                          {{ h2_gender }}
                        </option>
                        <option>MALE</option>
                        <option>FEMALE</option>
                      </select>

                      <button
                        @click="patch(gender)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Civil Status</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_civilstatus }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'civilstatus'">
                    <button
                      @click="isEdit = 'civilstatus'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'civilstatus'">
                    <div class="flex">
                      <select
                        v-model="civilstatus"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                      >
                        <option value="" selected disabled hidden>
                          {{ h2_civilstatus }}
                        </option>
                        <option>SINGLE</option>
                        <option>MARRIED</option>
                        <option>WIDOW</option>
                      </select>

                      <button
                        @click="patch(civilstatus)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Religion</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_religion }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'relserial'">
                    <button
                      @click="isEdit = 'relserial'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'relserial'">
                    <div class="flex">
                      <select
                        v-model="relserial"
                        id="religionSelect"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                      >
                        <option value="" selected disabled hidden>
                          {{ h2_religion }}
                        </option>
                        <option
                          v-for="religionOptions in religionOptions"
                          :value="religionOptions.relserial"
                          :key="religionOptions.relserial"
                        >
                          {{ religionOptions.relname }}
                        </option>
                      </select>

                      <button
                        @click="patch(relserial)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Dialect</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_dialect }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'diaserial'">
                    <button
                      @click="isEdit = 'diaserial'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'diaserial'">
                    <div class="flex">
                      <select
                        v-model="diaserial"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                      >
                        <option value="" selected disabled hidden>
                          {{ h2_dialect }}
                        </option>
                        <option
                          v-for="dialectOptions in dialectOptions"
                          :value="dialectOptions.diaserial"
                          :key="dialectOptions.diaserial"
                        >
                          {{ dialectOptions.dianame }}
                        </option>
                      </select>

                      <button
                        @click="patch(diaserial)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Origin of Birth</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_origin }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'origin'">
                    <button
                      @click="isEdit = 'origin'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'origin'">
                    <div class="flex">
                      <input
                        v-model="origin"
                        id="origin"
                        type="text"
                        maxlength="255"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Enter Origin"
                      />
                      <button
                        @click="patch(origin)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Address</h2>
                </div>
                <div class="basis-1/2">
                  <div class="flex flex-col md:flex-row">
                    <h6 class="font-normal text-slate-500">
                      {{ h2_puroksitio }}
                    </h6>
                    <h6 class="font-normal text-slate-500">
                      {{ h2_barangay }}
                    </h6>
                    <h6 class="font-normal text-slate-500">
                      {{ h2_province }}
                    </h6>
                  </div>
                </div>
                <div class="basis-1/4 flex flex-row justify-end">
                  <div v-show="isEdit != 'address'">
                    <button
                      @click="isEdit = 'address'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'address'">
                    <div class="flex">
                      <div class="flex flex-col mr-2">
                        <select
                          v-model="province"
                          @change="getMunicipality()"
                          class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        >
                          <option value="" selected disabled hidden>
                            {{ h2_province }}
                          </option>
                          <option
                            v-for="provinceOptions in provinceOptions"
                            :value="provinceOptions.provCode"
                            :key="provinceOptions.provCode"
                          >
                            {{ provinceOptions.provDesc }}
                          </option>
                        </select>
                        <select
                          v-model="municipality"
                          @change="getBarangay()"
                          class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3 my-2"
                        >
                          <option value="" selected disabled hidden>
                            {{ h2_municipality }}
                          </option>
                          <option
                            v-for="municipalityOptions in municipalityOptions"
                            :value="municipalityOptions.citymunCode"
                            :key="municipalityOptions.citymunCode"
                          >
                            {{ municipalityOptions.citymunDesc }}
                          </option>
                        </select>
                        <select
                          v-model="barangay"
                          class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3 mb-2"
                        >
                          <option value="" selected disabled hidden>
                            {{ h2_barangay }}
                          </option>
                          <option
                            v-for="barangayOptions in barangayOptions"
                            :value="barangayOptions.brgyCode"
                            :key="barangayOptions.brgyCode"
                          >
                            {{ barangayOptions.brgyDesc }}
                          </option>
                        </select>
                        <input
                          v-model="puroksitio"
                          type="text"
                          class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                          placeholder="Enter purok/sitio name"
                        />
                      </div>
                      <button
                        @click="
                          patchAddress(
                            province,
                            municipality,
                            barangay,
                            puroksitio
                          )
                        "
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div v-show="currentTab === 2">
              <h2 class="text-2xl font-bold text-red-600">
                Content Unavailable
              </h2>
              <p class="text-red-600">This content is under construction.</p>
            </div>
            <div v-show="currentTab === 3">
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Father's Name</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_fathersname }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'fathersname'">
                    <button
                      @click="isEdit = 'fathersname'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'fathersname'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="fathersname"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(fathersname)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Father's Occupation</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_fathers_occupation }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'foccupation'">
                    <button
                      @click="isEdit = 'foccupation'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'foccupation'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="foccupation"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(foccupation)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Father's Monthly Income</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_fathers_income }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'fmonincome'">
                    <button
                      @click="isEdit = 'fmonincome'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'fmonincome'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="fmonincome"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(fmonincome)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Mother's Name</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_mothersname }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'mothersname'">
                    <button
                      @click="isEdit = 'mothersname'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'mothersname'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="mothersname"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(mothersname)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Mother's Occupation</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_mothers_occupation }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'moccupation'">
                    <button
                      @click="isEdit = 'moccupation'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'moccupation'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="moccupation"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(moccupation)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Mother's Monthly Income</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_mothers_income }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'mmonincome'">
                    <button
                      @click="isEdit = 'mmonincome'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'mmonincome'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="mmonincome"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(mmonincome)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Parent's Contact Number</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_parents_contact }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'parentscontact'">
                    <button
                      @click="isEdit = 'parentscontact'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'parentscontact'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="parentscontact"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(parentscontact)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Parent's Address</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_parents_address }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'parentsaddress'">
                    <button
                      @click="isEdit = 'parentsaddress'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'parentsaddress'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="parentsaddress"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(parentsaddress)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">No. of Siblings</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_noofsiblings }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'noofsiblings'">
                    <button
                      @click="isEdit = 'noofsiblings'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'noofsiblings'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="noofsiblings"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(noofsiblings)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Guardian's Name</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_guardiansname }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'guardiansname'">
                    <button
                      @click="isEdit = 'guardiansname'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'guardiansname'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="guardiansname"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(guardiansname)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Guardian's Contact Number</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_guardians_contact }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'gcontact'">
                    <button
                      @click="isEdit = 'gcontact'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'gcontact'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="gcontact"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(gcontact)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Guardian's Address</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_guardians_address }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'gaddress'">
                    <button
                      @click="isEdit = 'gaddress'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'gaddress'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="gaddress"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(gaddress)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div v-show="currentTab === 4">
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Previous School Name</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_schoollast }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'schoollast'">
                    <button
                      @click="isEdit = 'schoollast'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'schoollast'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="schoollast"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(schoollast)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Address</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_schooladdress }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'schooladdress'">
                    <button
                      @click="isEdit = 'schooladdress'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'schooladdress'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="schooladdress"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(schooladdress)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Year Graduated</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">
                    {{ h2_yeargraduated }}
                  </h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'yeargraduated'">
                    <button
                      @click="isEdit = 'yeargraduated'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'yeargraduated'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="yeargraduated"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(yeargraduated)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Average</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_average }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'average'">
                    <button
                      @click="isEdit = 'average'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'average'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="average"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(average)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div v-show="currentTab === 5">
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Learner Reference Number</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_lrn }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'lrnno'">
                    <button
                      @click="isEdit = 'lrnno'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'lrnno'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="lrnno"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(lrnno)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Email</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_emailadd }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'emailadd'">
                    <button
                      @click="isEdit = 'emailadd'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'emailadd'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="emailadd"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(emailadd)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Phone Number</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">{{ h2_contactno }}</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'contactno'">
                    <button
                      @click="isEdit = 'contactno'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'contactno'">
                    <div class="flex">
                      <input
                        type="text"
                        v-model="contactno"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patch(contactno)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
              <hr class="mt-3 mb-3" />
              <div class="flex flex-col md:flex-row">
                <div class="basis-1/4">
                  <h2 class="font-bold">Password</h2>
                </div>
                <div class="basis-1/2">
                  <h2 class="font-normal text-slate-500">••••••••</h2>
                </div>
                <div class="basis-1/4 flex flex-col md:flex-row justify-end">
                  <div v-show="isEdit != 'password'">
                    <button
                      @click="isEdit = 'password'"
                      class="flex items-center place-content-center bg-transparent text-blue-600 hover:underline hover:underline-offset-auto"
                    >
                      <RedoDot class="w-4 h-4 mr-2" />
                      <span>Edit</span>
                    </button>
                  </div>
                  <div v-show="isEdit === 'password'">
                    <div class="flex">
                      <input
                        type="password"
                        v-model="password"
                        class="border-gray-400 focus:border-blue-500 focus:outline-none py-2 px-3 block w-full rounded-lg bg-slate-100 mr-3"
                        placeholder="Type here..."
                      />
                      <button
                        @click="patchPassword(password)"
                        class="flex items-center place-content-center bg-transparent text-[#1C1AAB] hover:underline hover:underline-offset-auto"
                      >
                        <CheckCircle2 class="w-8 h-8 mr-1" />
                      </button>
                      <button
                        @click="isEdit = ''"
                        class="flex items-center place-content-center bg-transparent text-red-500 hover:underline hover:underline-offset-auto ml-2"
                      >
                        <XCircle class="w-8 h-8" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
