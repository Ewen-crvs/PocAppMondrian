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
          <div class="text-center mt-4">
            <p class="text-white text-xl">Temps restant : {{ timeLeft }}s</p>
          </div>

          <!-- Question -->
          <div class="bg-[#F0DA9C] mt-6 p-6 rounded-xl" v-if="!showTransitionScreen">
            <p>{{ currentQuestion.title }}</p>
          </div>

          <!-- Réponses -->
          <div v-if="!showMessage && !showTransitionScreen" class="mt-6 space-y-6 px-6">
            <button
                v-for="(answer, index) in currentQuestion.answers"
                :key="index"
                @click="checkAnswer(answer)"
                class="flex w-full justify-center rounded-md bg-[#F1ECD4] px-3 py-1.5 text-sm font-semibold leading-6 text-black shadow-sm hover:bg-yellow-200"
            >
              {{ answer }}
            </button>
          </div>

          <!-- Écran de transition -->
          <div v-if="showTransitionScreen" class="mt-6 rounded-md bg-blue-50 p-4">
            <div class="text-center">
              <h3 class="text-sm font-medium text-blue-800">Veuillez patienter, la prochaine question arrive...</h3>
            </div>
          </div>

          <!-- Message pour réponse correcte ou incorrecte -->
          <div v-if="showMessage && !showTransitionScreen" class="mt-6 rounded-md" :class="goodResponse ? 'bg-green-50' : 'bg-red-50'">
            <div class="p-4">
              <div class="text-center">
                <h3 class="text-sm font-medium" :class="goodResponse ? 'text-green-800' : 'text-red-800'">
                  {{ goodResponse ? 'Bonne réponse !' : 'Mauvaise réponse !' }}
                </h3>
                <p class="mt-2 text-sm" :class="goodResponse ? 'text-green-700' : 'text-red-700'">{{ message }}</p>
              </div>
            </div>
          </div>

          <!-- Bouton suivant -->
          <div v-if="showNextButton && !showTransitionScreen" class="mt-10">
            <button @click="nextQuestion" class="w-full bg-[#F0DA9C] text-black font-bold py-2 px-4 rounded">
              Suivant
            </button>
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
let currentQuestionIndex = ref(0);
let currentQuestion = ref(questions[currentQuestionIndex.value]);
let showMessage = ref(false);
let goodResponse = ref(false);
let lastResponse = ref(false);
let message = ref('');
let showNextButton = ref(false);
let timeLeft = ref(10); // Timer initialisé à 10 secondes
let timer: number | undefined;
let showTransitionScreen = ref(false); // Pour l'écran de transition

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
        showMessage.value = true;
        setTimeout(() => showTransitionScreen.value = true, 10000);
      }
      setTimeout(() => nextQuestion(), 10000); // Passer à la question suivante après 2s
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
  //clearInterval(timer); // Arrêter le timer une fois la réponse donnée
  //showTransitionScreen.value = true; // Afficher l'écran de transition
  //setTimeout(() => nextQuestion(), 3000);
}

// Fonction pour passer à la question suivante
function nextQuestion() {
  showMessage.value = false;
  showNextButton.value = false;
  showTransitionScreen.value = false;

  if (currentQuestionIndex.value < questions.length - 1) {
    currentQuestionIndex.value++;
    currentQuestion.value = questions[currentQuestionIndex.value];
    startTimer(); // Redémarrer le timer pour la prochaine question
  } else {
    message.value = "Félicitations, vous avez terminé le jeu !";
    showMessage.value = true;
    lastResponse.value = true;
    showNextButton.value = false;
  }
}
</script>
