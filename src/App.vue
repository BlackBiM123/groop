<script setup>
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Subscribe from './components/Subscribe.vue'
import Features from './components/Features.vue'
import ListBlock from './components/ListBlock.vue'
import Tasks from './components/Tasks.vue'
import TeamBlock from './components/TeamBlock.vue'
import Pricing from './components/Pricing.vue'
import Footer from './components/Footer.vue'
import Analytics from "./components/Analytics.vue";

import { watch } from 'vue';
import { usePreferredLanguages } from '@vueuse/core';
import {useI18n} from "vue-i18n";

const preferredLanguages = usePreferredLanguages();
const { locale } = useI18n();

watch(preferredLanguages, (languages) => {
  if (languages.includes('ru')) {
    locale.value = 'ru';
  } else {
    locale.value = 'en';
  }
}, { immediate: true });

</script>

<template>
  <div class="app">
    <Header />
    <Hero />
    <Subscribe />
    <Features />
    <ListBlock />
    <Tasks />
    <TeamBlock />
    <Analytics />
    <Pricing />
    <Footer />
  </div>
</template>



