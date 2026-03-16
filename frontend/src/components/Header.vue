<script setup lang="ts">
import BetaversionLabel from '@/components/BetaversionLabel.vue'

interface Props {
  isHome: boolean
}

defineProps<Props>()
const emit = defineEmits(['reset'])
</script>

<template>
  <header>
    <div class="rvo-layout-column">
      <div class="rvo-topnav__background rvo-topnav__background--horizontal-rule">
        <div class="rvo-max-width-layout rvo-max-width-layout--md rvo-max-width-layout-inline-padding--sm">
          <nav class="rvo-topnav rvo-topnav--lg">
            <ul class="rvo-topnav__list">
              <li class="rvo-topnav__item" style="margin-right: auto">
                <BetaversionLabel />
              </li>
              <li v-if="!isHome" class="rvo-topnav__item">
                <a
                  class="rvo-link rvo-topnav__link rvo-link--logoblauw"
                  style="cursor: pointer;"
                  @click="$emit('reset')"
                >
                  <span
                    class="utrecht-icon rvo-icon rvo-icon-terug rvo-icon--lg rvo-icon--wit"
                    role="img"
                    aria-label="Terug"
                  ></span>
                  Begin opnieuw
                </a>
              </li>
              <li v-else style="height: 48px"></li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
  </header>
</template>
