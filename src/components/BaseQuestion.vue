<script setup>
defineProps(['isButtonHidden', 'isButtonDisabled', 'onNext', 'id'])
</script>

<template>
  <div class="wrapper" :id="id">
    <div class="content">
      <h2 class="heading">
        <slot name="heading"></slot>
      </h2>

      <p class="description">
        <slot name="description"></slot>
      </p>

      <slot></slot>

      <button
        class="btn-next"
        :disabled="isButtonDisabled"
        :hidden="isButtonHidden"
        @click="onNext"
      >
        <slot name="button-text">Næste</slot>
      </button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.wrapper {
  padding-inline: 2em;
  min-height: 75vh;
  display: flex;
  align-items: center;
  justify-content: center;
  scroll-snap-align: center;

  .content {
    width: 100%;
  }

  &:not(.active) {
    opacity: 0.25;
    pointer-events: none;
  }

  .heading {
    font-size: 1.5rem;
    font-weight: bold;
  }

  .description {
    font-size: 1rem;
    margin-bottom: 3em;
  }

  .btn-next {
    cursor: pointer;
    margin-top: 3rem;
    margin-inline: auto;
    min-width: 300px;
    display: block;
    padding-top: 1rem;
    padding-bottom: 1rem;
    border-radius: 4px;
    border: 0;
    outline: 0;
    background-color: #000000;
    font-weight: bold;
    color: white;
    text-align: center;
    font-size: 1rem;
    transition: 300ms;

    @media (max-width: 767px) {
      width: 100%;
    }

    &:hover {
      opacity: 0.85;
    }

    &[disabled] {
      pointer-events: none;
      background-color: #a9acc7;
      color: white;
    }

    &[hidden] {
      visibility: hidden;
    }
  }
}
</style>
