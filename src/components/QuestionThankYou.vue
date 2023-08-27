<script setup>
import BaseQuestion from './BaseQuestion.vue'
import logoGoogle from '../assets/images/logo-google.png'
import logoTrustpilot from '../assets/images/logo-trustpilot.png'

const props = defineProps(['onNext', 'id', 'nextId'])
</script>

<template>
  <BaseQuestion :id="id">
    <template #heading>Tak fordi du ville hjælpe</template>
    <template #description>
      Vi er glade for, at du har været tilfreds med din oplevelse. Det vil betyde meget for os, hvis
      du vil dele din oplevelse med andre.
    </template>

    <div class="button-wrapper">
      <a href="https://google.com" target="_blank">
        <img :src="logoGoogle" />
        <span>Google</span>
      </a>
      <a href="https://trustpilot.com" target="_blank">
        <img :src="logoTrustpilot" />
        <span>Trustpilot</span>
      </a>
    </div>
  </BaseQuestion>
</template>

<style scoped lang="scss">
:deep(.heading) {
  text-align: center;
}

:deep(.description) {
  text-align: center;
  margin-bottom: 2em !important;
}

:deep(.btn-next) {
  display: none !important;
}

.button-wrapper {
  display: flex;
  align-items: center;
  column-gap: 1em;

  a {
    flex: 1;
    cursor: pointer;
    padding: 0.75rem 1.5rem;
    border-radius: 4px;
    border: 0;
    outline: 0;
    background-color: #000000;
    color: white;
    font-size: 1rem;
    font-weight: bold;
    transition: 300ms;
    display: flex;
    align-items: center;
    justify-content: center;
    column-gap: 0.75em;

    img {
      width: 24px;
      height: 24px;
    }

    span {
      display: block;
      line-height: 100%;
    }

    &:hover {
      opacity: 0.85;
    }
  }
}
</style>
