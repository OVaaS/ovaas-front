<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

defineProps<{
  loading: boolean
  isDisabled: boolean
}>()

defineEmits(['click'])

</script>

<template>
  <button class="bg-white border border-gray-300 dark:bg-gray-100 hover:bg-gray-50 dark:hover:bg-gray-200 text-gray-800 font-bold py-1.5 px-3.5 rounded-lg inline-flex shadow-sm items-center focus:outline-none" :disabled="isDisabled" :class="{ 'opacity-50 cursor-not-allowed': isDisabled }" @click="$emit('click', $event)">
    <div class="inline-flex items-center justify-center mr-2 -ml-1 h-7 w-7">
      <bx-bx-refresh v-if="loading" class="text-2xl sm:animate-spin" />
      <bx-bx-cloud-upload v-else class="text-2xl" />
    </div>
    {{ t('upload.recognize') }}
  </button>
</template>
