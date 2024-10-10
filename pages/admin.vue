<template>
  <div class="bg-[#404040] bg-cover bg-center w-auto h-auto">
    <div class="bg-[url('/public/assets/image2.svg')] bg-cover bg-center w-auto h-auto">
      <div class="pb-20 bg-gray-700/50 bg-cover bg-center w-auto h-auto">
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
                <button class="mr-2 rounded-md bg-[#F1ECD4] px-3 py-1.5 text-sm font-semibold leading-6 text-black shadow-sm hover:bg-yellow-200">Editer</button>
                <button class="rounded-md bg-[#F1ECD4] px-3 py-1.5 text-sm font-semibold leading-6 text-black shadow-sm hover:bg-red-500">Supprimer</button>
              </div>
            </div>
            <p>{{ question.title }}</p>
          </div>
          <div class="mt-12">
            <button class="w-full justify-center rounded-md bg-[#F1ECD4] px-3 py-1.5 text-sm font-semibold leading-6 text-black shadow-sm hover:bg-yellow-200">Créer un contenu</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import questions from '../public/data/questions.json';
</script>
