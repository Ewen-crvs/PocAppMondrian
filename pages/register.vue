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
                  <label for="email" class="block text-sm font-medium leading-6 text-white">Nom</label>
                  <div class="mt-2">
                    <input class="block w-full bg-slate-900/70 rounded-md border-0 py-1.5 text-gray-200 shadow-sm placeholder:text-gray-400 sm:text-sm sm:leading-6" />
                  </div>
                </div>

                <div class="mt-6">
                  <label for="password" class="block text-sm font-medium leading-6 text-white">Prénom</label>
                  <div class="mt-2 mb-2">
                    <input class="block w-full bg-slate-900/70 rounded-md border-0 py-1.5 text-gray-200 shadow-sm placeholder:text-gray-400 sm:text-sm sm:leading-6" />
                  </div>
                </div>

                <div class="mt-12">
                  <NuxtLink to="/script">
                    <button class="flex w-full justify-center rounded-md bg-slate-900/70 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Commencer</button>
                  </NuxtLink>
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
</script>