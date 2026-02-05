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
  <div class="min-h-screen flex flex-col">
    <UHeader>
      <template #left>
        <NuxtLink to="/" class="flex items-center gap-2 font-bold text-xl mr-4">
          <UIcon name="i-lucide-graduation-cap" class="w-8 h-8 text-primary-500" />
          <span>SmartSchool</span>
        </NuxtLink>
      </template>

      <UNavigationMenu :items="items" />

      <template #right>
        <UColorModeButton />

        <div class="flex gap-2">
          <UButton to="/auth/login" label="Log in" color="neutral" variant="ghost" />
          <UButton to="/auth/register" label="Get Started" color="primary" variant="solid" />
        </div>
      </template>

      <template #body>
        <UNavigationMenu :items orientation="vertical" class="-mx-2.5" />
      </template>
    </UHeader>

    <UMain class="grow">
      <slot />
    </UMain>

    <UFooter>
      <template #left>
        <p class="text-sm text-muted">
          © {{ new Date().getFullYear() }} SmartSchool. All rights reserved.
        </p>
      </template>
      <template #right>
        <div>
          <UButton icon="i-simple-icons-github" color="neutral" variant="ghost" to="https://github.com/miumerfarooq/school-management-system-frontend-nuxtjs" target="_blank" />
        </div>
      </template>
    </UFooter>
  </div>
</template>
