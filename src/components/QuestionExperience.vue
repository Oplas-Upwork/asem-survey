<script setup>
import { ref } from 'vue'
import BaseQuestion from './BaseQuestion.vue'
import expressionActive1 from '../assets/images/expression-active-1.svg'
import expressionActive2 from '../assets/images/expression-active-2.svg'
import expressionActive3 from '../assets/images/expression-active-3.svg'
import expressionActive4 from '../assets/images/expression-active-4.svg'
import expressionActive5 from '../assets/images/expression-active-5.svg'

import expression1 from '../assets/images/expression-1.svg'
import expression2 from '../assets/images/expression-2.svg'
import expression3 from '../assets/images/expression-3.svg'
import expression4 from '../assets/images/expression-4.svg'
import expression5 from '../assets/images/expression-5.svg'

const expressions = [
  {
    imageSrcActive: expressionActive1,
    imageSrc: expression1,
    rate: 1
  },
  {
    imageSrcActive: expressionActive2,
    imageSrc: expression2,
    rate: 2
  },
  {
    imageSrcActive: expressionActive3,
    imageSrc: expression3,
    rate: 3
  },
  {
    imageSrcActive: expressionActive4,
    imageSrc: expression4,
    rate: 4
  },
  {
    imageSrcActive: expressionActive5,
    imageSrc: expression5,
    rate: 5
  }
]

const props = defineProps(['onNext', 'id', 'nextId'])

const selectedExpression = ref(null)

const handleNext = () => {
  props.onNext({
    id: props.id,
    nextId: props.nextId,
    value: selectedExpression.value
  })
}
</script>

<template>
  <BaseQuestion :is-button-hidden="selectedExpression === null" :on-next="handleNext" :id="id">
    <template #heading> Hvordan var din oplevelse?</template>

    <div class="emoji-selection">
      <div
        v-for="expression in expressions"
        :key="expression.rate"
        class="item"
        @click="selectedExpression = expression.rate"
      >
        <img
          :src="expression.imageSrcActive"
          :style="{ display: selectedExpression === expression.rate ? 'block' : 'none' }"
        />
        <img
          :src="expression.imageSrc"
          :style="{ display: selectedExpression === expression.rate ? 'none' : 'block' }"
        />
      </div>
    </div>

    <span class="note">Din feedback er anonymt</span>
  </BaseQuestion>
</template>

<style scoped lang="scss">
:deep(.heading) {
  text-align: center;
}

:deep(.description) {
  margin-bottom: 2em !important;
}

.emoji-selection {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  max-width: 340px;
  margin-inline: auto;

  img {
    margin-inline: auto;
    max-width: 50px;
    max-height: 50px;
    cursor: pointer;
  }
}

.note {
  margin-top: 2em;
  display: block;
  font-size: 0.875rem;
  text-align: center;
  color: #5d5d5d;
}
</style>
