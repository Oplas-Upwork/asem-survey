<script setup>
import { ref } from 'vue'
import BaseQuestion from './BaseQuestion.vue'

const selections = ['Behandling', 'Kommunikation', 'Pris', 'Ventetid', 'Betjening', 'Andet']

const props = defineProps(['onNext', 'id', 'nextId'])

const inputName = ref('')
const inputPhoneNumber = ref('')
const inputEmail = ref('')

const handleNext = () => {
  props.onNext({
    id: props.id,
    nextId: props.nextId,
    value: {
      name: inputName.value,
      phoneNumber: inputPhoneNumber.value,
      email: inputEmail.value
    }
  })
}
</script>

<template>
  <BaseQuestion :is-button-disabled="inputName === ''" :on-next="handleNext" :id="id">
    <template #heading>Vi har ikke været gode nok</template>
    <template #description>Ønsker du at blive kontaktet af butikschefen? </template>

    <input placeholder="Navn" v-model="inputName" />
    <input placeholder="Telefonnummer" v-model="inputPhoneNumber" />
    <input placeholder="Email" v-model="inputEmail" />

    <template #button-text>Kontakt mig </template>
  </BaseQuestion>
</template>

<style scoped lang="scss">
:deep(.btn-next) {
  margin-inline-end: 0 !important;
  margin-top: 1rem !important;
}

:deep(.description) {
  margin-bottom: 1em !important;
}

input {
  margin-top: 1rem;
  width: 100%;
  padding: 1em;
  font-size: 1rem;
  color: #33475b;
  border: 1px solid #acacac;
  border-radius: 4px;
  background-color: white;
  font-family: Roboto;
  font-size: 1rem;
  outline: 0;
}
</style>
