<template>
  <div class="bg-[#404040] bg-cover bg-center w-auto h-auto">
    <div class="pb-20 bg-[url('/public/assets/image2.svg')] bg-cover bg-center w-auto h-auto">
      <div class="bg-gray-700/50 bg-cover bg-center w-auto h-auto">
        <div class="max-w-xs mx-auto">
          <!-- Logo -->
          <div class="justify-center flex pt-10">
            <img src="../public/assets/logo_mondrian.svg">
          </div>

          <!-- Questions -->
          <div class="bg-[#F0DA9C] mt-6 p-6 rounded-xl" v-for="(question, questionIndex) in questions">
            <div class="flex justify-between">
              <p>Q.{{ questionIndex + 1 }}:</p>
              <div class="flex">
                <button class="mr-2 rounded-md bg-slate-900/70 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Editer</button>
                <button class="rounded-md bg-slate-900/70 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-red-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Supprimer</button>
              </div>
            </div>
            <p>{{ question.title }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import questions from '../public/data/questions.json';
</script>
