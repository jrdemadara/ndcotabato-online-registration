<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'
import heroImage from '../assets/bg_register.png'
import successImage from '../assets/bg_success.png'
import { ArrowRight, ArrowLeft, Check } from 'lucide-vue-next'
import confetti from 'canvas-confetti'
import flatPickr from 'vue-flatpickr-component'
import 'flatpickr/dist/flatpickr.css'

const router = useRouter()
const year = new Date().getFullYear()
const currentStep = ref(1)

//* Inputs Initialization
const errors1 = ref({})
const errors2 = ref({})
const errors3 = ref({})
const errors4 = ref({})
const lastname = ref('')
const firstname = ref('')
const middlename = ref('')
const extension = ref('')
const birthdate = ref('')
const gender = ref('')
const civilstatus = ref('')
const religion = ref('')
const dialect = ref('')
const origin = ref('')
const province = ref('')
const municipality = ref('')
const barangay = ref('')
const puroksitio = ref('')
const fathersname = ref('')
const fathers_occupation = ref('')
const fathers_income = ref('')
const mothersname = ref('')
const mothers_occupation = ref('')
const mothers_income = ref('')
const parents_contact = ref('')
const parents_address = ref('')
const noofsiblings = ref('')
const guardiansname = ref('')
const guardians_contact = ref('')
const guardians_address = ref('')
const schoollast = ref('')
const schooladdress = ref('')
const yeargraduated = ref('')
const average = ref('')
const lrn = ref('')
const emailadd = ref('')
const contactno = ref('')
const password = ref('')
const confirm_password = ref('')
// Options Data
const provinceOptions = ref([])
const religionOptions = ref([])
const dialectOptions = ref([])
const municipalityOptions = ref([])
const barangayOptions = ref([])

// Populate Dependency
onMounted(async () => {
  try {
    const response = await axios.get(
      'https://ndparang.info/api/v1/uri/province',
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
      'https://ndparang.info/api/v1/uri/municipality',
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
      'https://ndparang.info/api/v1/uri/barangay',
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

const restrictParentPhone = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 11)
  parents_contact.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 11) {
    event.target.blur()
  }
}

const restrictGuardianPhone = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 11)
  guardians_contact.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 11) {
    event.target.blur()
  }
}

const restrictMyPhone = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 11)
  contactno.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 11) {
    event.target.blur()
  }
}

const restrictFatherIncome = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 11)
  fathers_income.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 11) {
    event.target.blur()
  }
}

const restrictMotherIncome = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 11)
  mothers_income.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 11) {
    event.target.blur()
  }
}

const restrictLRN = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 12)
  lrn.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 12) {
    event.target.blur()
  }
}

const restrictYear = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 4)
  yeargraduated.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 4) {
    event.target.blur()
  }
}

const restrictAverage = (event) => {
  const sanitizedValue = event.target.value.replace(/\D/g, '')
  const restrictedValue = sanitizedValue.slice(0, 2)
  average.value = restrictedValue
  // Disable typing when 11 digits are reached
  if (restrictedValue.length === 2) {
    event.target.blur()
  }
}

function validateSteps() {
  if (currentStep.value === 1) {
    errors1.value = {}
    if (!lastname.value) {
      errors1.value.lastname = 'Lastname is required'
    }
    if (!firstname.value) {
      errors1.value.firstname = 'Firstname is required'
    }
    if (!middlename.value) {
      errors1.value.middlename = 'Middlename is required'
    }
    if (!birthdate.value) {
      errors1.value.birthdate = 'Birthdate is required'
    }
    if (!gender.value) {
      errors1.value.gender = 'Gender is required'
    }
    if (!civilstatus.value) {
      errors1.value.civilstatus = 'civil Status is required'
    }
    if (!religion.value) {
      errors1.value.religion = 'Religion is required'
    }
    if (!dialect.value) {
      errors1.value.dialect = 'Dialect is required'
    }
    if (!origin.value) {
      errors1.value.origin = 'Origin is required'
    }
    if (!province.value) {
      errors1.value.province = 'Province is required'
    }
    if (!municipality.value) {
      errors1.value.municipality = 'Municipality is required'
    }
    if (!barangay.value) {
      errors1.value.barangay = 'Barangay is required'
    }
    if (!puroksitio.value) {
      errors1.value.puroksitio = 'Purok is required'
    }
    if (Object.keys(errors1.value).length === 0) {
      currentStep.value++
    }
    if (Object.keys(errors1.value).length > 0) {
      console.log(errors1.value)
    }
  } else if (currentStep.value === 2) {
    errors2.value = {}
    if (!fathersname.value) {
      errors2.value.fathersname = 'Father name is required'
    }
    if (!fathers_occupation.value) {
      errors2.value.fathers_occupation = 'Father name is required'
    }
    if (!fathers_income.value) {
      errors2.value.fathers_income = 'Father name is required'
    }
    if (!mothersname.value) {
      errors2.value.mothersname = 'Mother name is required'
    }
    if (!mothers_occupation.value) {
      errors2.value.mothers_occupation = 'Mother occupation is required'
    }
    if (!mothers_income.value) {
      errors2.value.mothers_income = 'Mother income is required'
    }
    if (!parents_contact.value) {
      errors2.value.parents_contact = 'Parents contact is required'
    }
    if (!parents_address.value) {
      errors2.value.parents_address = 'Parents address is required'
    }
    if (!noofsiblings.value) {
      errors2.value.noofsiblings = 'No. of siblings is required'
    }
    if (Object.keys(errors2.value).length === 0) {
      currentStep.value++
    } else {
      console.log(errors2.value)
    }
  } else if (currentStep.value === 3) {
    errors3.value = {}
    if (!schoollast.value) {
      errors3.value.schoollast = 'Last school attended name is required'
    }
    if (!schooladdress.value) {
      errors3.value.schooladdress = 'Address is required'
    }
    if (!yeargraduated.value) {
      errors3.value.yeargraduated = 'Year graduated is required'
    }
    if (!average.value) {
      errors3.value.average = 'Average is required'
    }
    if (Object.keys(errors3.value).length === 0) {
      currentStep.value++
    }
  } else if (currentStep.value === 4) {
    errors4.value = {}
    if (!lrn.value) {
      errors4.value.lrn = 'Learner Reference Number is required'
    }
    if (!emailadd.value) {
      errors4.value.emailadd = 'Email Address is required'
    }
    if (!contactno.value) {
      errors4.value.contactno = 'Contact Number is required'
    }
    if (!password.value) {
      errors4.value.password = 'Password is required'
    }
    if (!confirm_password.value) {
      errors4.value.confirm_password = 'Confirm Password is required'
    }
    if (password.value != confirm_password.value) {
      errors4.value.confirm_password = "Password didn't match"
    }
    if (Object.keys(errors4.value).length === 0) {
      currentStep.value++
    }
  }
}

async function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms))
}

async function register() {
  try {
    currentStep.value = 'processing'

    await delay(1500)
    const response = await axios.post(
      'https://ndparang.info/api/v1/uri/register',
      {
        lrn: lrn.value,
        password: password.value,
        lastname: lastname.value,
        firstname: firstname.value,
        middlename: middlename.value,
        extension: extension.value,
        birthdate: birthdate.value,
        gender: gender.value,
        civilstatus: civilstatus.value,
        contactno: contactno.value,
        email: emailadd.value,
        religion: religion.value,
        dialect: dialect.value,
        origin: origin.value,
        province: province.value,
        municipality: municipality.value,
        barangay: barangay.value,
        puroksitio: puroksitio.value,
        fathersname: fathersname.value,
        fathers_occupation: fathers_occupation.value,
        fathers_income: fathers_income.value,
        mothersname: mothersname.value,
        mothers_occupation: mothers_occupation.value,
        mothers_income: mothers_income.value,
        parents_contact: parents_contact.value,
        parents_address: parents_address.value,
        noofsiblings: noofsiblings.value,
        guardiansname: guardiansname.value,
        guardians_contact: guardians_contact.value,
        guardians_address: guardians_address.value,
        schoollast: schoollast.value,
        schooladdress: schooladdress.value,
        yeargraduated: yeargraduated.value,
        average: average.value
      }
    )
    const status = await response.status
    if (status === 200) {
      shootConfetti()
    }
  } catch (error) {
    if (error.response.status == 409) {
      currentStep.value = 'conflict'
    } else {
      router.push('/error')
    }
  }
}

//* Success confetti
function shootConfetti() {
  currentStep.value = 'complete'
  let duration = 15 * 1000
  let animationEnd = Date.now() + duration
  let defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 }

  function randomInRange(min, max) {
    return Math.random() * (max - min) + min
  }

  let interval = setInterval(function () {
    let timeLeft = animationEnd - Date.now()

    if (timeLeft <= 0) {
      return clearInterval(interval)
    }

    let particleCount = 50 * (timeLeft / duration)
    // since particles fall down, start a bit higher than random
    confetti(
      Object.assign({}, defaults, {
        particleCount,
        origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 }
      })
    )
    confetti(
      Object.assign({}, defaults, {
        particleCount,
        origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 }
      })
    )
  }, 250)
}
</script>

<style scoped>
.confetti-canvas {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
}
</style>

<template>
  <div v-cloak>
    <div
      v-show="
        currentStep != 'complete' &&
        currentStep != 'conflict' &&
        currentStep != 'processing'
      "
    >
      <div class="relative">
        <!-- Background image -->
        <div
          class="h-screen md:h-screen bg-cover bg-center bg-no-repeat"
          :style="{ backgroundImage: `url(${heroImage})` }"
        ></div>
        <div class="absolute inset-0 flex flex-col items-center">
          <img
            src="@/assets/ndparang_logo.png"
            class="h-20 md:h-24 mt-5 md:mt-5"
            alt="logo"
          />
          <a
            href="#"
            class="hidden md:block text-white font-semibold text-2xl mt-2"
            >Notre Dame of Parang Inc.</a
          >
          <div class="flex justify-center mt-5 md:mt-8">
            <div v-if="currentStep === 1">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-[#8CB369] hover:bg-[#96CB66]"
              >
                1
              </button>
            </div>
            <div v-else-if="currentStep > 1">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                1
              </button>
            </div>
            <div v-else-if="currentStep < 1">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                1
              </button>
            </div>

            <div v-if="currentStep === 2">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-[#8CB369] hover:bg-[#96CB66]"
              >
                2
              </button>
            </div>
            <div v-else-if="currentStep > 2">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                2
              </button>
            </div>
            <div v-else-if="currentStep < 2">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                2
              </button>
            </div>

            <div v-if="currentStep === 3">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-[#8CB369] hover:bg-[#96CB66]"
              >
                3
              </button>
            </div>
            <div v-else-if="currentStep > 3">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                3
              </button>
            </div>
            <div v-else-if="currentStep < 3">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                3
              </button>
            </div>

            <div v-if="currentStep === 4">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-[#8CB369] hover:bg-[#96CB66]"
              >
                4
              </button>
            </div>
            <div v-else-if="currentStep > 4">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                4
              </button>
            </div>
            <div v-else-if="currentStep < 4">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                4
              </button>
            </div>

            <div v-if="currentStep === 5">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-[#8CB369] hover:bg-[#96CB66]"
              >
                5
              </button>
            </div>
            <div v-else-if="currentStep > 5">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                5
              </button>
            </div>
            <div v-else-if="currentStep < 5">
              <button
                @click="validateSteps"
                class="w-10 h-10 rounded-full text-white mx-2 bg-slate-400 hover:bg-slate-500"
              >
                5
              </button>
            </div>
          </div>
          <div class="px-5 mt-5 mb-3 md:mt-8">
            <div class="font-medium text-center text-white text-xl">
              <div v-if="currentStep === 1">Setup Your Profile</div>
              <div v-if="currentStep === 2">Parents/Guardian Information</div>
              <div v-if="currentStep === 3">Previous School Attended</div>
              <div v-if="currentStep === 4">Setup Security Credentials</div>
              <div v-if="currentStep === 5">Information Review</div>
            </div>
            <div
              class="hidden md:block lg:block text-slate-400 text-center mt-2"
            >
              <div v-if="currentStep === 1">
                To start off, please enter your personal information.
              </div>
              <div v-if="currentStep === 2">
                Please enter your parents/guardian information.
              </div>
              <div v-if="currentStep === 3">
                Please state your previous school.
              </div>
              <div v-if="currentStep === 4">
                Please setup your login credentials.
              </div>
              <div v-if="currentStep === 5">
                Please review the information you provided.
              </div>
            </div>
            <hr class="mt-2" />
          </div>

          <form @submit.prevent="submitForm" class="space-y-4 overflow-auto">
            <div v-show="currentStep === 1">
              <div
                class="w-screen grid grid-cols-12 gap-4 gap-y-3.5 mt-5 md:mt-8 px-6 md:mx-4 md:px-56 mb-8 md:mb-10 h-96 md:h-fit"
              >
                <div class="col-span-12 sm:col-span-3">
                  <label
                    for="lastname"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Lastname</label
                  >
                  <input
                    v-model="lastname"
                    id="lastname"
                    type="text"
                    :class="{ 'border border-red-500': errors1.lastname }"
                    maxlength="255"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter Lastname"
                  />
                </div>
                <div class="col-span-12 sm:col-span-3">
                  <label
                    for="firstname"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Firstname</label
                  >
                  <input
                    v-model="firstname"
                    id="firstname"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors1.firstname }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter Firstname"
                  />
                </div>
                <div class="col-span-12 sm:col-span-3">
                  <label
                    for="middlename"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Middlename</label
                  >
                  <input
                    v-model="middlename"
                    id="middlename"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors1.middlename }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter Middlename"
                  />
                </div>
                <div class="col-span-12 sm:col-span-3">
                  <label
                    for="extension"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Extrension</label
                  >
                  <input
                    v-model="extension"
                    id="extension"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors1.extension }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter Extension (optional)"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="birthdate"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Birthdate</label
                  >
                  <flat-pickr
                    v-model="birthdate"
                    :config="config"
                    :class="{ 'border border-red-500': errors1.birthdate }"
                    class="datepicker w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Select birthdate"
                    name="date"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="gender"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Gender</label
                  >
                  <select
                    v-model="gender"
                    id="gender"
                    :class="{ 'border border-red-500': errors1.gender }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Gender
                    </option>
                    <option>Male</option>
                    <option>Female</option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="civilstatus"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Civil Status</label
                  >
                  <select
                    v-model="civilstatus"
                    id="civilstatus"
                    :class="{ 'border border-red-500': errors1.civilstatus }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Civil Status
                    </option>
                    <option>Single</option>
                    <option>Married</option>
                    <option>Widow</option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="religion"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Religion</label
                  >
                  <select
                    v-model="religion"
                    id="religion"
                    :class="{ 'border border-red-500': errors1.religion }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Religion
                    </option>
                    <option
                      v-for="religionOptions in religionOptions"
                      :value="religionOptions.relserial"
                      :key="religionOptions.relserial"
                    >
                      {{ religionOptions.relname }}
                    </option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="dialect"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Dialect</label
                  >
                  <select
                    v-model="dialect"
                    id="dialect"
                    :class="{ 'border border-red-500': errors1.dialect }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Dialect
                    </option>
                    <option
                      v-for="dialectOptions in dialectOptions"
                      :value="dialectOptions.diaserial"
                      :key="dialectOptions.diaserial"
                    >
                      {{ dialectOptions.dianame }}
                    </option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="origin"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Origin of Birth</label
                  >
                  <input
                    v-model="origin"
                    id="origin"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors1.origin }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                    placeholder="Enter Origin"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="province"
                    class="font-normal text-sm mb-1 text-gray-400 blockl"
                    >Province</label
                  >
                  <select
                    v-model="province"
                    id="province"
                    @change="getMunicipality()"
                    :class="{ 'border border-red-500': errors1.province }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Province
                    </option>
                    <option
                      v-for="provinceOptions in provinceOptions"
                      :value="provinceOptions.provCode"
                      :key="provinceOptions.provCode"
                    >
                      {{ provinceOptions.provDesc }}
                    </option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="municipality"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Municipality</label
                  >
                  <select
                    v-model="municipality"
                    id="municipality"
                    @change="getBarangay()"
                    :class="{ 'border border-red-500': errors1.municipality }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Municipality
                    </option>
                    <option
                      v-for="municipalityOptions in municipalityOptions"
                      :value="municipalityOptions.citymunCode"
                      :key="municipalityOptions.citymunCode"
                    >
                      {{ municipalityOptions.citymunDesc }}
                    </option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="barangay"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Barangay</label
                  >
                  <select
                    v-model="barangay"
                    id="barangay"
                    :class="{ 'border border-red-500': errors1.barangay }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-gray-500 font-normal"
                  >
                    <option value="" selected disabled hidden>
                      Select Barangay
                    </option>
                    <option
                      v-for="barangayOptions in barangayOptions"
                      :value="barangayOptions.brgyCode"
                      :key="barangayOptions.brgyCode"
                    >
                      {{ barangayOptions.brgyDesc }}
                    </option>
                  </select>
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="puroksitio"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Purok</label
                  >
                  <input
                    v-model="puroksitio"
                    id="puroksitio"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors1.puroksitio }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter purok/sitio name"
                  />
                </div>
              </div>
            </div>
            <div v-show="currentStep === 2">
              <div
                class="w-screen grid grid-cols-12 gap-4 gap-y-3.5 mt-5 md:mt-8 px-6 md:mx-4 md:px-56 mb-5 md:mb-10 h-96 md:h-fit"
              >
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="fathersname"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Father's Name</label
                  >
                  <input
                    v-model="fathersname"
                    id="fathersname"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors2.fathersname }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter father's name"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="fathers_occupation"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Father's Occupation</label
                  >
                  <input
                    v-model="fathers_occupation"
                    id="fathers_occupation"
                    type="text"
                    maxlength="255"
                    :class="{
                      'border border-red-500': errors2.fathers_occupation
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter father's occupation"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="fathers_income"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Father's Monthly Income</label
                  >
                  <input
                    v-model="fathers_income"
                    id="fathers_income"
                    type="number"
                    @input="restrictFatherIncome"
                    :class="{ 'border border-red-500': errors2.fathers_income }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter father's monthly income"
                  />
                </div>

                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="mothersname"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Mother's Name</label
                  >
                  <input
                    v-model="mothersname"
                    id="mothersname"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors2.mothersname }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter mother's name"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="mothers_occupation"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Mother's Occupation</label
                  >
                  <input
                    v-model="mothers_occupation"
                    id="mothers_occupation"
                    type="text"
                    maxlength="255"
                    :class="{
                      'border border-red-500': errors2.mothers_occupation
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter mother's occupation"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="mothers_income"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Mother's Monthly Income</label
                  >
                  <input
                    v-model="mothers_income"
                    id="mothers_income"
                    type="number"
                    @input="restrictMotherIncome"
                    maxlength="11"
                    :class="{ 'border border-red-500': errors2.mothers_income }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter mother's monthly income"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="parents_contact"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Parent's Contact Number</label
                  >
                  <input
                    v-model="parents_contact"
                    id="parents_contact"
                    type="number"
                    @input="restrictParentPhone"
                    :class="{
                      'border border-red-500': errors2.parents_contact
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter parent's contact number"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="parents_address"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Parent's Address</label
                  >
                  <input
                    v-model="parents_address"
                    id="parents_address"
                    type="text"
                    maxlength="255"
                    :class="{
                      'border border-red-500': errors2.parents_address
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter parent's address"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="noofsiblings"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Number of Siblings</label
                  >
                  <input
                    v-model="noofsiblings"
                    id="noofsiblings"
                    type="number"
                    :class="{ 'border border-red-500': errors2.noofsiblings }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter number of siblings"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="guardiansname"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Guardian's Name</label
                  >
                  <input
                    v-model="guardiansname"
                    id="guardiansname"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors2.guardiansname }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter guardian's name(optional)"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="guardians_contact"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Guardian's Contact Number</label
                  >
                  <input
                    v-model="guardians_contact"
                    id="gcontact"
                    type="number"
                    @input="restrictGuardianPhone"
                    :class="{
                      'border border-red-500': errors2.guardians_contact
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter guardian's contact number(optional)"
                  />
                </div>
                <div class="col-span-12 sm:col-span-4">
                  <label
                    for="guardians_address"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Guardian's Address</label
                  >
                  <input
                    v-model="guardians_address"
                    id="gaddress"
                    type="text"
                    maxlength="255"
                    :class="{
                      'border border-red-500': errors2.guardians_address
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter guardian's address(optional)"
                  />
                </div>
              </div>
            </div>
            <div v-show="currentStep === 3">
              <div
                class="w-screen grid grid-cols-12 gap-4 gap-y-3.5 mt-5 md:mt-8 px-6 md:mx-4 md:px-56 mb-5 md:mb-10 h-96 md:h-fit"
              >
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="schoollast"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Previous School Name</label
                  >
                  <input
                    v-model="schoollast"
                    id="schoollast"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors3.schoollast }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter previous school"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="schooladdress"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Previous School Address</label
                  >
                  <input
                    v-model="schooladdress"
                    id="schooladdress"
                    type="text"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors3.schooladdress }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter school address"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="yeargraduated"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Year Graduated</label
                  >
                  <input
                    v-model="yeargraduated"
                    id="yeargraduated"
                    type="number"
                    @input="restrictYear"
                    :class="{ 'border border-red-500': errors3.yeargraduated }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter year graduated"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="average"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Average</label
                  >
                  <input
                    v-model="average"
                    id="average"
                    type="number"
                    @input="restrictAverage"
                    :class="{ 'border border-red-500': errors3.average }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter average grade"
                  />
                </div>
              </div>
            </div>
            <div v-show="currentStep === 4">
              <div
                class="w-screen grid grid-cols-12 gap-4 gap-y-3.5 mt-5 md:mt-8 px-6 md:mx-4 md:px-56 mb-5 md:mb-10 h-96 md:h-fit"
              >
                <div class="col-span-12 sm:col-span-12">
                  <label
                    for="lrn"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Learner Reference Number</label
                  >
                  <input
                    v-model="lrn"
                    id="lrn"
                    type="number"
                    @input="restrictLRN"
                    :class="{ 'border border-red-500': errors4.lrn }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter your LRN"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="emailadd"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Email</label
                  >
                  <input
                    v-model="emailadd"
                    id="emailadd"
                    type="email"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors4.emailadd }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter your email"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="contactno"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Phone</label
                  >
                  <input
                    v-model="contactno"
                    id="contactno"
                    type="number"
                    @input="restrictMyPhone"
                    :class="{ 'border border-red-500': errors4.contactno }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter your phone number"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="password"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Password</label
                  >
                  <input
                    v-model="password"
                    id="password"
                    type="password"
                    maxlength="255"
                    :class="{ 'border border-red-500': errors4.password }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Enter your password"
                  />
                </div>
                <div class="col-span-12 sm:col-span-6">
                  <label
                    for="confirm_password"
                    class="font-normal text-sm mb-1 text-gray-400 block"
                    >Confirm Password</label
                  >
                  <input
                    v-model="confirm_password"
                    id="confirm_password"
                    type="password"
                    maxlength="255"
                    :class="{
                      'border border-red-500': errors4.confirm_password
                    }"
                    class="w-full px-2 py-3 bg-gray-400 bg-opacity-20 backdrop-blur-sm rounded-md shadow-sm focus:outline-1 text-white font-normal"
                    placeholder="Confirm password"
                  />
                </div>
              </div>
            </div>
            <div v-show="currentStep === 5">
              <h2 class="text-xl font-bold text-white text-center px-2 mt-10">
                You can review the information you
                <br />
                provided by clicking the
                <span class="text-[#8CB369]">previous</span> button.
              </h2>
              <p class="text-[#8CB369] text-center mt-4 px-2 w-full">
                By clicking the proceed button, You hereby declare that the
                information you provided is true and correct.
              </p>
            </div>
          </form>
        </div>

        <div class="absolute flex flex-col items-center bottom-0">
          <div
            class="flex flex-row self-center md:self-center mt-5 md:mt-10 md:px-56"
          >
            <div v-if="currentStep > 1">
              <button
                @click="currentStep--"
                class="w-40 bg-slate-500 hover:bg-slate-600 text-white font-normal py-2.5 px-4 rounded-md flex items-center place-content-center mr-6 self-start"
              >
                <ArrowLeft class="w-4 h-4 mr-2" />
                <span>Previous</span>
              </button>
            </div>
            <div v-if="currentStep < 5">
              <button
                @click="validateSteps"
                class="w-40 bg-[#8CB369] hover:bg-[#96CB66] text-white font-normal py-2.5 rounded-md flex items-center place-content-center self-end"
              >
                <span>Next</span>
                <ArrowRight class="w-4 h-4 ml-2" />
              </button>
            </div>
            <div v-if="currentStep === 5">
              <button
                @click="register"
                class="w-40 bg-[#8CB369] hover:bg-[#96CB66] text-white font-normal py-2.5 rounded-md flex items-center place-content-center"
              >
                <span>Proceed</span>
                <Check class="w-4 h-4 ml-2" />
              </button>
            </div>
          </div>
          <div class="bg-gray-950 bg-opacity-60 w-screen mt-5">
            <div
              class="text-slate-400 text-center flex justify-center py-2 md:py-6"
            >
              © {{ year }} Notre Dame of Parang Inc.
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-if="currentStep === 'processing'">
      <div class="relative">
        <!-- Background image -->
        <div
          class="h-screen md:h-screen bg-cover bg-center bg-no-repeat"
          :style="{ backgroundImage: `url(${heroImage})` }"
        ></div>
        <div class="absolute inset-0 flex flex-col items-center">
          <img
            src="@/assets/ndparang_logo.png"
            class="h-20 md:h-24 mt-5 md:mt-12"
            alt="logo"
          />
          <a href="#" class="md:block text-white font-semibold text-lg mt-2"
            >Notre Dame of Parang Inc.</a
          >
          <span class="relative flex h-10 w-10 mt-10">
            <span
              class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[#96CB66] opacity-75"
            ></span>
            <span
              class="relative inline-flex rounded-full h-10 w-10 bg-[#8CB369]"
            ></span>
          </span>
          <h2
            class="text-xl md:text-2xl font-bold text-[#8CB369] text-center px-2 mt-8"
          >
            processing...
          </h2>
        </div>
        <div class="bg-gray-950 bg-opacity-60 w-screen mt-5">
          <div
            class="text-slate-400 text-center flex justify-center py-2 md:py-6"
          >
            © {{ year }} Notre Dame of Parang Inc.
          </div>
        </div>
      </div>
    </div>

    <div v-if="currentStep === 'conflict'">
      <div class="relative">
        <!-- Background image -->
        <div
          class="h-screen md:h-screen bg-cover bg-center bg-no-repeat"
          :style="{ backgroundImage: `url(${heroImage})` }"
        ></div>
        <div class="absolute inset-0 flex flex-col items-center">
          <img
            src="@/assets/ndparang_logo.png"
            class="h-20 md:h-24 mt-5 md:mt-10"
            alt="logo"
          />
          <a href="#" class="md:block text-white font-semibold text-lg mt-2"
            >Notre Dame of Parang Inc.</a
          >
          <img class="mt-20 w-28" src="@/assets/conflict.svg" />
          <h2
            class="text-2xl md:text-2xl font-bold text-red-600 text-center px-2 mt-8"
          >
            Data Found: It Already Exists!
          </h2>
          <p class="text-slate-300 text-center mt-2 px-2 md:text-lg">
            Apologies, but the LRN, name, email, or phone number you provided is
            already registered. <br />
            Login using your existing credentials to access your profile.
          </p>
          <button
            class="w-40 bg-[#8CB369] hover:bg-[#96CB66] text-white font-normal py-2.5 px-4 rounded-md flex items-center place-content-center mt-10"
          >
            <router-link to="/"><span>Login</span></router-link>
          </button>
        </div>
        <div class="bg-gray-950 bg-opacity-60 w-screen mt-5">
          <div
            class="text-slate-400 text-center flex justify-center py-2 md:py-6"
          >
            © {{ year }} Notre Dame of Parang Inc.
          </div>
        </div>
      </div>
    </div>

    <div v-if="currentStep === 'complete'">
      <div class="relative">
        <!-- Background image -->
        <div
          class="h-screen md:h-screen bg-cover bg-center bg-no-repeat"
          :style="{ backgroundImage: `url(${successImage})` }"
        ></div>
        <div class="absolute inset-0 flex flex-col items-center">
          <img
            src="@/assets/ndparang_logo.png"
            class="h-20 md:h-24 mt-5 md:mt-10"
            alt="logo"
          />
          <a href="#" class="md:block text-white font-semibold text-lg mt-2"
            >Notre Dame of Parang Inc.</a
          >
          <div class="absolute">
            <canvas ref="canvas" class="confetti-canvas"></canvas>
          </div>
          <img class="mt-20 w-28" src="@/assets/success.svg" />
          <h2
            class="text-2xl md:text-2xl font-bold text-[#8CB369] text-center px-2 mt-8"
          >
            Registration Success!
          </h2>
          <p class="text-slate-300 text-center mt-2 px-2 md:text-lg">
            Thank you for choosing NDU! We are thrilled to have you on board.
            <br />
            You can now login to your profile.
          </p>
          <button
            class="w-40 bg-[#8CB369] hover:bg-[#96CB66] text-white font-normal py-2.5 px-4 rounded-md flex items-center place-content-center mt-10"
          >
            <router-link to="/"><span>Login</span></router-link>
          </button>
        </div>
        <div class="bg-gray-950 bg-opacity-60 w-screen mt-5">
          <div
            class="text-slate-400 text-center flex justify-center py-2 md:py-6"
          >
            © {{ year }} Notre Dame of Parang Inc.
          </div>
        </div>
      </div>
    </div>
    <div
      class="w-fit h-fit absolute inset-0 mt-5 md:mt-32 lg:mt-32 ml-6 md:ml-16 lg:ml-52"
    >
      <a href="#" class="text-slate-400 font-normal text-base">
        <router-link to="/">
          <div class="flex flex-row items-center hover:text-[#8CB369]">
            <ArrowLeft class="w-8 h-8 md:w-6 md:h-6 mr-2" />
            <span
              class="hidden md:inline-block text-slate-400 hover:text-[#8CB369] font-normal text-sm"
            >
              Back to login
            </span>
          </div>
        </router-link>
      </a>
    </div>
  </div>
</template>
