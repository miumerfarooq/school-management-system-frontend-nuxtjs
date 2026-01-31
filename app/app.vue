<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui';

const items = ref<NavigationMenuItem[]>([
  {
    label: 'Home',
    icon: 'i-lucide-house',
    to: '/',
  },
  {
    label: 'About',
    icon: 'i-lucide-book-open',
    to: '/about'
  },
  {
    label: 'Contact Us',
    icon: 'i-lucide-contact-round',
    to: '/contact'
  }
])
</script>

<template>
  <UApp>
    <!-- Markup shared across all pages, ex: NavBar -->
    <UNavigationMenu :items="items" />
    <!-- Markup shared across all pages, ex: NavBar -->
    <NuxtPage />
  </UApp>
</template>
