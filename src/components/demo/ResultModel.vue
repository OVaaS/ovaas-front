<template>
  <div v-if="open" class="absolute z-20 object-cover w-full h-full bg-gray-800 bg-opacity-50">
    <div class="relative flex items-center justify-center h-full text-5xl font-semibold text-white md:text-6xl">
      {{ text || t('demos.handwritten-ocr.text-not-found') }}
      <div class="absolute top-0 right-0 p-6 text-lg">
        <div class="inline-flex items-center justify-center w-10 h-10 text-gray-800 bg-gray-100 border border-gray-500 rounded-full hover:bg-opacity-75 dark:(bg-gray-800 text-white)" @click="emit('update:open', false)">
          <ion-close-round />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

defineProps<{
  open: boolean
  text?: string
}>()

const emit = defineEmits(['update:open'])
</script>
