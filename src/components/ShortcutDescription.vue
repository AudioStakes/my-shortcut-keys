<script setup lang="ts">
import Key from '@/components/Key.vue'
import GameKey from '@/stores/game-key'
import { injectStrict } from '@/utils/inject-strict'
import Keyboard from '@/utils/keyboard'

const {
  wordsOfDescriptionFilledByCorrectKeys,
  wordsOfDescriptionFilledByPressedKeys,
} = injectStrict(GameKey)

withDefaults(defineProps<{ isFillInBlankMode?: boolean }>(), {
  isFillInBlankMode: false,
})
</script>

<template>
  <div
    class="flex flex-wrap justify-center items-center align-center space-x-2"
  >
    <div
      v-for="(word, index) in isFillInBlankMode
        ? wordsOfDescriptionFilledByPressedKeys
        : wordsOfDescriptionFilledByCorrectKeys"
      :key="index"
    >
      <Key
        v-if="Keyboard.isKey(word) || word === ''"
        :key-name="word"
        class="scale-[0.8]"
      ></Key>
      <span v-else class="text-xl">{{ word }}</span>
    </div>
  </div>
</template>
