<template>
  <div class="bg-[url('/public/assets/image1.svg')] bg-cover bg-center w-auto h-screen">
    <div class="bg-gray-700/50 bg-cover bg-center w-auto h-screen">
      <div class="max-w-xs mx-auto">
        <div class="justify-center flex pt-10">
          <img src="../public/assets/logo_mondrian.svg">
        </div>
        <div>
          <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-[480px]">
            <div class="bg-slate-800/50 px-6 py-12 shadow sm:rounded-lg sm:px-12 rounded-xl">
              <form method="POST">
                <div>
                  <label class="block text-sm font-medium leading-6 text-white">Nom</label>
                  <div class="mt-2">
                    <input v-model="lastName" class="px-2 block w-full bg-slate-900/70 rounded-md border-0 py-1.5 text-gray-200 shadow-sm placeholder:text-gray-400 sm:text-sm sm:leading-6" />
                  </div>
                </div>

                <div class="mt-6">
                  <label class="block text-sm font-medium leading-6 text-white">Prénom</label>
                  <div class="mt-2 mb-2">
                    <input v-model="firstName" class="px-2 block w-full bg-slate-900/70 rounded-md border-0 py-1.5 text-gray-200 shadow-sm placeholder:text-gray-400 sm:text-sm sm:leading-6" />
                  </div>
                </div>

                <div class="mt-12">
                  <button @click.prevent="onSubmit()" class="flex w-full justify-center rounded-md bg-[#F1ECD4] px-3 py-1.5 text-sm font-semibold leading-6 text-black shadow-sm hover:bg-yellow-200">Commencer</button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { useRouter } from 'vue-router'
import { ref } from 'vue'

const router = useRouter()
const firstName = ref('')
const lastName = ref('')

function onSubmit() {
  if (firstName.value == 'admin' && lastName.value == 'admin') {
    router.push({ path: '/admin' })
  } else {
    router.push({ path: '/script' })
  }
}
</script>