<script setup lang="ts">
import type { Answer, Source } from '@/models/DecisionTree'

interface Props {
  questionId: string
  question: string
  explanation: string
  answers: Answer[]
  sources?: Source[]
  isFirst: boolean
}

defineProps<Props>()
defineEmits<{
  answered: [answer: Answer]
  back: []
}>()
</script>

<template>
  <div class="rvo-max-width-layout--md">
    <div class="rvo-layout-margin-vertical--s">
      <fieldset
        class="rvo-max-width-layout--sm utrecht-form-fieldset rvo-form-fieldset border-none"
        style="width: 600px; max-width: 100%;"
      >
        <!-- Question -->
        <div class="flex">
          <h1 class="utrecht-heading-3">{{ question }}</h1>
        </div>

        <!-- Explanation -->
        <div v-if="explanation" style="margin-bottom: 1.5rem;">
          <p style="white-space: pre-line" class="utrecht-paragraph">{{ explanation }}</p>
        </div>

        <!-- Answers -->
        <div>
          <!-- Column layout for 3+ answers -->
          <div v-if="answers.length > 2">
            <ul class="rvo-layout-column rvo-layout-gap--sm no-list">
              <li v-for="(answer, index) in answers" :key="index">
                <button
                  type="button"
                  @click="$emit('answered', answer)"
                  class="utrecht-button utrecht-button--secondary-action utrecht-button--rvo-md rvo-link--no-underline rvo-link--hover"
                  style="width: 100%; text-align: left;"
                >
                  {{ answer.answer }}
                </button>
              </li>
            </ul>
          </div>

          <!-- Row layout for 1-2 answers -->
          <div v-else class="rvo-layout-row rvo-layout-gap--sm">
            <button
              v-for="(answer, index) in answers"
              :key="index"
              type="button"
              @click="$emit('answered', answer)"
              class="utrecht-button utrecht-button--secondary-action utrecht-button--rvo-md rvo-link--no-underline rvo-link--hover"
            >
              {{ answer.answer }}
            </button>
          </div>
        </div>
      </fieldset>

        <!-- Sources -->
        <div v-if="sources && sources.length > 0" style="margin-top: 1.5rem;">
          <p class="utrecht-paragraph rvo-text--sm"><strong>Bron:</strong>
            <span v-for="(src, index) in sources" :key="index">
              <a v-if="src.url" :href="src.url" target="_blank" rel="noopener noreferrer" class="rvo-link">{{ src.source }}</a>
              <span v-else>{{ src.source }}</span>
              <span v-if="index < sources.length - 1">, </span>
            </span>
          </p>
        </div>

      <!-- Navigation -->
      <div
        style="justify-content: flex-start; margin-top: 2rem;"
        class="rvo-layout-row rvo-layout-gap--md"
      >
        <button
          v-if="!isFirst"
          @click="$emit('back')"
          type="button"
          class="flex utrecht-button utrecht-button--secondary-action rvo-layout-row rvo-layout-gap--md utrecht-button--rvo-md rvo-link--no-underline"
        >
          <span
            class="utrecht-icon rvo-icon rvo-icon-terug rvo-icon--lg rvo-icon--wit"
            role="img"
            aria-label="Terug"
          ></span>
          Vorige vraag
        </button>
      </div>
    </div>
  </div>
</template>
