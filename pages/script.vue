<template>
  <div class="bg-[#404040] bg-cover bg-center w-auto h-screen">
    <div class="bg-[url('/public/assets/image2.svg')] bg-cover bg-center w-auto h-screen">
      <div class="bg-gray-700/50 bg-cover bg-center w-auto h-screen">
        <div class="max-w-xs mx-auto">
          <!-- Logo -->
          <div class="justify-center flex pt-10">
            <img src="../public/assets/logo_mondrian.svg">
          </div>

          <!-- Timer -->
          <div v-if="!showMessage && timeLeft > 3" class="flex justify-center mt-7">
            <span class="inline-flex items-center rounded-md bg-gray-300/10 px-2 py-1 text-sm font-medium text-gray-300 ring-1 ring-inset ring-gray-300/20">Temps restant : {{ timeLeft }}s</span>
          </div>
          <div v-if="!showMessage && timeLeft <= 3" class="flex justify-center mt-7">
            <span class="inline-flex items-center rounded-md bg-red-400/10 px-2 py-1 text-sm font-medium text-red-400 ring-1 ring-inset ring-red-400/20">Temps restant : {{ timeLeft }}s</span>
          </div>

          <!-- Question -->
          <div v-if="!lastResponse" class="bg-[#F0DA9C] mt-6 p-6 rounded-xl">
            <p>{{ currentQuestion.title }}</p>
          </div>

          <!-- Réponses -->
          <div v-if="!showMessage" class="mt-6 space-y-6 px-6">
            <button
                v-for="(answer, index) in currentQuestion.answers"
                :key="index"
                @click="checkAnswer(answer)"
                class="flex w-full justify-center rounded-md bg-[#F1ECD4] px-3 py-1.5 text-sm font-semibold leading-6 text-black shadow-sm hover:bg-yellow-200"
            >
              {{ answer }}
            </button>
          </div>

          <!-- Message pour réponse correcte ou incorrecte -->
          <div v-if="showMessage && !lastResponse" class="mt-6 rounded-md" :class="goodResponse ? 'bg-green-50' : 'bg-red-50'">
            <div class="p-4">
              <div class="text-center">
                <h3 class="text-sm font-medium" :class="goodResponse ? 'text-green-800' : 'text-red-800'">
                  {{ goodResponse ? 'Bonne réponse !' : 'Dommage...' }}
                </h3>
                <p class="mt-2 text-sm" :class="goodResponse ? 'text-green-700' : 'text-red-700'">{{ message }}</p>
              </div>
            </div>
          </div>

          <div v-if="showMessage && lastResponse">
            <div class="bg-green-50 mt-12 rounded-md">
              <div class="p-4">
                <div class="text-center">
                  <h3 class="text-sm font-medium text-green-800">
                    {{ message }}
                  </h3>
                </div>
              </div>
            </div>
            <div class="mt-12">
              <NuxtLink to="/">
                <button class="flex w-full justify-center rounded-md bg-slate-900/70 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Retourner au Menu</button>
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import questions from '../public/data/questions.json';

// Déclaration des variables
let currentQuestionIndex = ref(9);
let currentQuestion = ref(questions[currentQuestionIndex.value]);
let showMessage = ref(false);
let goodResponse = ref(false);
let lastResponse = ref(false);
let message = ref('');
let timeLeft = ref(10);
let timer: number | undefined;

// Démarrer le timer quand le composant est monté
onMounted(() => {
  startTimer();
});

// Nettoyage du timer si on quitte le composant
onBeforeUnmount(() => {
  clearInterval(timer);
});

// Fonction pour démarrer le timer
function startTimer() {
  timeLeft.value = 10; // Réinitialiser le timer
  timer = setInterval(() => {
    if (timeLeft.value > 0) {
      timeLeft.value--;
    } else {
      clearInterval(timer);
      if (!showMessage.value) {
        message.value = currentQuestion.value.complement;
        showMessage.value = true;
      }
      setTimeout(() => nextQuestion(), 10000); // Passer à la question suivante après 10s
      clearInterval(timer);
    }
  }, 1000);
}

// Fonction pour vérifier la réponse choisie
function checkAnswer(answer: string) {
  if (answer === currentQuestion.value.right_answer) {
    message.value = currentQuestion.value.complement;
    goodResponse.value = true;
  } else {
    message.value = currentQuestion.value.complement;
    goodResponse.value = false;
  }
}

// Fonction pour passer à la question suivante
function nextQuestion() {
  showMessage.value = false;

  if (currentQuestionIndex.value < questions.length - 1) {
    currentQuestionIndex.value++;
    currentQuestion.value = questions[currentQuestionIndex.value];
    startTimer(); // Redémarrer le timer pour la prochaine question
  } else {
    message.value = "Félicitations, vous avez terminé le jeu !";
    showMessage.value = true;
    lastResponse.value = true;
  }
}
</script>
