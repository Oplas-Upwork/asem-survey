<script setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import QuestionExperience from './QuestionExperience.vue'
import QuestionUserSelection from './QuestionUserSelection.vue'
import QuestionRatingLowStep1 from './QuestionRatingLowStep1.vue'
import QuestionRatingLowStep2 from './QuestionRatingLowStep2.vue'
import QuestionThankYou from './QuestionThankYou.vue'

const questions = {
  QuestionUserSelection: 'UserSelection',
  QuestionExperience: 'Experience',
  QuestionRatingLowStep1: 'RatingLowStep1',
  QuestionRatingLowStep2: 'RatingLowStep2',
  QuestionRatingHigh: 'RatingHigh',
  QuestionThankYou: 'ThankYou'
}

const handleNext = ({ id, nextId, value }) => {
  const nextElement = document.querySelector('#' + nextId)
  nextElement.classList.add('active')
  nextElement.scrollIntoView({ behavior: 'smooth', block: 'center' })
}

// const showQuestion = (id, to = 'up') => {}

// const hideQuestion = (id, to = 'up') => {
//   // gsap.to(`#${id}`, {
//   //   y: '-100',
//   //   duration: 0.25,
//   //   opacity: 0
//   // })
// }
</script>

<template>
  <QuestionUserSelection
    :on-next="handleNext"
    :id="questions.QuestionUserSelection"
    :nextId="questions.QuestionExperience"
    class="active"
  />
  <QuestionExperience
    :on-next="handleNext"
    :id="questions.QuestionExperience"
    :nextId="questions.QuestionRatingLowStep1"
  />
  <QuestionRatingLowStep1
    :on-next="handleNext"
    :id="questions.QuestionRatingLowStep1"
    :nextId="questions.QuestionRatingLowStep2"
  />
  <QuestionRatingLowStep2
    :on-next="handleNext"
    :id="questions.QuestionRatingLowStep2"
    :nextId="questions.QuestionThankYou"
  />
  <QuestionThankYou :id="questions.QuestionThankYou" />
</template>
