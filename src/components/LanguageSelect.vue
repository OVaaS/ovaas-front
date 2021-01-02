<template>
  <div class="relative h-full">
    <div class="text-white h-full flex items-center text-2xl px-3 md:px-5" @mouseenter="show = true">
      <vs-language />
    </div>
    <transition name="slide-fade">
      <div v-show="show" class="absolute top-0 right-0 pt-14 pr-2" @mouseleave="show = false">
        <div class="bg-white dark:bg-gray-700 inline-flex flex-col rounded-md p-1.5 shadow-md">
          <button
            v-for="lang in langs"
            :key="lang.locale"
            class=" w-full text-center rounded-md hover:bg-gray-200 dark:hover:bg-gray-600 focus:outline-none px-3 py-1 focus:text-gray-500 dark:focus:text-gray-400"
            :value="lang.locale"
            :selected="lang.locale === currentLang"
            @click="currentLang = lang.locale"
          >
            {{ lang.name }}
          </button>
        </div>
      </div>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { computed, watch, ref, defineProps, defineEmit } from 'vue'
import { useI18n } from 'vue-i18n'
import { languages as langs } from '/~/messages'
import { usePreferredLanguages } from '@vueuse/core'
import { localeSchema } from '../logics'

const show = ref(false)

const props = defineProps({
  modelValue: {
    type: String,
    require: true,
  },
})

const emit = defineEmit(['update:modelValue'])

const preferredLang = usePreferredLanguages()
const { locale } = useI18n()

const currentLang = computed<string>({
  get() {
    return localeSchema.value ? localeSchema.value : localeSchema.value = preferredLang.value[0] === 'ja' ? 'ja' : 'en'
  },
  set(v) {
    localeSchema.value = v
  },
})

watch(currentLang, (v) => {
  if (typeof document !== 'undefined')
    document.documentElement.lang = v
  locale.value = v
},
{ immediate: true })
</script>

<style>
.slide-fade-leave-active,
.slide-fade-enter-active {
  transition: all 0.2s ease-out;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}
</style>