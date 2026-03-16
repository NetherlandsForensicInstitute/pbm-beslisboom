<script setup lang="ts">
import type { Source } from '@/models/DecisionTree'

interface Props {
  sources: Source[] | undefined
}

defineProps<Props>()
</script>

<template>
  <div>
    <ul class="no-list">
      <li v-for="(source, index) in sources" :key="index" class="text-sm flex items-center">
        <span
          class="utrecht-icon rvo-icon rvo-icon-info rvo-icon--xl rvo-status-icon-info"
          role="img"
          aria-label="Info"
        ></span>
        <a v-if="source.url" :href="source.url" target="_blank" rel="noopener noreferrer" class="rvo-link utrecht-link">
          {{ source.source }}
        </a>
        <span v-else class="rvo-link--no-underline">
          {{ source.source }}
        </span>
      </li>
    </ul>
  </div>
</template>
