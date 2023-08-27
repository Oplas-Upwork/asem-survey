<script setup>
import userImage from '../assets/user-placeholder.png'
import { ref } from 'vue'
import BaseQuestion from './BaseQuestion.vue'

const users = [
  {
    imageSrc: userImage,
    name: 'Lisbeth H.'
  },
  {
    imageSrc: userImage,
    name: 'Lone Stilhoff'
  },
  {
    imageSrc: userImage,
    name: 'Anita Strarup'
  },
  {
    imageSrc: userImage,
    name: 'Alli Bouloum'
  },
  {
    imageSrc: userImage,
    name: 'Sofie Steiness'
  },
  {
    imageSrc: userImage,
    name: 'Ved ikke'
  }
]

const props = defineProps(['onNext', 'id', 'nextId'])

const selectedUser = ref('')

const handleNext = () => {
  props.onNext({
    id: props.id,
    nextId: props.nextId,
    value: selectedUser.value
  })
}
</script>

<template>
  <BaseQuestion :is-button-disabled="selectedUser.length === 0" :on-next="handleNext" :id="id">
    <template #heading>Tak fordi du vil hjælpe os</template>
    <template #description>Hvem har du været til konsultation hos?</template>

    <div class="user-selection">
      <div
        v-for="user in users"
        :key="user.name"
        class="item"
        :class="{ active: selectedUser === user.name }"
        @click="selectedUser = user.name"
      >
        <div class="image-wrapper">
          <img :src="user.imageSrc" />

          <div class="icon-check">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12.75l6 6 9-13.5" />
            </svg>
          </div>
        </div>

        <span>{{ user.name }}</span>
      </div>
    </div>
  </BaseQuestion>
</template>

<style scoped lang="scss">
.user-selection {
  margin-top: 2em;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 1em;
  row-gap: 2em;

  .item {
    cursor: pointer;

    &.active {
      .image-wrapper {
        img {
          border-color: #000000;
        }
        .icon-check {
          display: block;
        }
      }

      span {
        font-weight: bold;
      }
    }

    .image-wrapper {
      --size: 75px;
      position: relative;
      width: var(--size);
      height: var(--size);
      margin-inline: auto;

      @media (max-width: 767px) {
        --size: 65px;
      }

      img {
        width: var(--size);
        height: var(--size);
        object-fit: cover;
        border-radius: 50%;
        border: 4px solid #e9ebef;
        transition: border-color 150ms;
      }

      .icon-check {
        padding: 4px;
        width: 27px;
        height: 27px;
        border-radius: 50%;
        color: white;
        background-color: #000000;

        @media (max-width: 767px) {
          padding: 2px;
          width: 24px;
          height: 24px;
        }

        display: none;
        position: absolute;
        right: 0;
        top: 0;
      }
    }

    span {
      margin-block-start: 0.5em;
      display: block;
      text-align: center;
      transition: font-weight 150ms;

      @media (max-width: 767px) {
        font-size: 0.85rem;
      }
    }
  }
}
</style>
