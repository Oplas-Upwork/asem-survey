<script setup>
import { ref } from 'vue'
import BaseQuestion from './BaseQuestion.vue'

const selections = ['Behandling', 'Kommunikation', 'Pris', 'Ventetid', 'Betjening', 'Andet']

const props = defineProps(['onNext', 'id', 'nextId'])

const selectedItem = ref(null)

const handleNext = () => {
  props.onNext({
    id: props.id,
    nextId: props.nextId,
    value: selectedItem.value
  })
}
</script>

<template>
  <BaseQuestion :is-button-disabled="selectedItem === null" :on-next="handleNext" :id="id">
    <template #heading>Hvad var der galt?</template>
    <template #description>Du kan vælge flere end en.</template>

    <div class="selection">
      <div
        v-for="selection in selections"
        :key="selection"
        class="item"
        :class="{ active: selectedItem === selection }"
        @click="selectedItem = selection"
      >
        {{ selection }}
      </div>
    </div>

    <textarea rows="6" placeholder="Du kan skrive din kommentar her"></textarea>

    <template #button-text>Afslut</template>
  </BaseQuestion>
</template>

<style scoped lang="scss">
:deep(.btn-next) {
  margin-top: 0.5em !important;
}

:deep(.description) {
  margin-bottom: 2em !important;
}

.selection {
  display: flex;
  flex-wrap: wrap;
  gap: 1em;

  .item {
    padding: 0.625em 1.25em;
    border: 1px solid #33475b;
    border-radius: 100px;
    font-size: 1rem;
    font-weight: bold;
    color: #33475b;
    cursor: pointer;
    transition: 150ms;

    &.active,
    &:hover {
      color: white;
      background-color: #191919;
      border-color: #191919;
    }
  }
}

textarea {
  margin-top: 1.5rem;
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
