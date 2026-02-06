<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui';

defineProps<{
  mode: 'drawer' | 'slideover' | 'modal'
}>()

const items: NavigationMenuItem[][] = [
  [
    {
      label: 'Home',
      icon: 'i-lucide-house',
      active: true
    },{
      label: 'Inbox',
      icon: 'i-lucide-inbox',
      badge: 4
    },{
      label: 'Contacts',
      icon: 'i-lucide-users'
    },{
      label: 'Settings',
      icon: 'i-lucide-settings',
      defaultOpen: true,
      children: [
        { label: 'General' },
        { label: 'Member' },
        { label: 'Notification' }
      ]
    }
  ],
  [
    {
      label: 'Feedback',
      icon: 'i-lucide-message-circle',
      to: 'https://github.com/miumerfarooq/school-management-system-frontend-nuxtjs',
      target: '_blank'
    },{
      label: 'Help & Support',
      icon: 'i-lucide-info',
      to: 'https://github.com/miumerfarooq/',
      target: '_blank'
    }
  ]
]
</script>

<template>
  <div>
    <UDashboardGroup>
      <UDashboardSidebar :mode="'drawer'" collapsible resizable :ui="{ footer: 'border-t border-default' }">
        <template #header="{ collapsed }">
          <NuxtLink v-if="!collapsed" to="/" class="flex items-center gap-2 font-bold text-xl mr-4">
            <UIcon name="i-lucide-graduation-cap" class="w-8 h-8 text-primary-500" />
            <span>SmartSchool</span>
          </NuxtLink>
          <NuxtLink v-else to="/" class="flex items-center gap-2 font-bold text-xl mr-4">
            <UIcon name="i-lucide-graduation-cap" class="w-8 h-8 text-primary-500" />
          </NuxtLink>
        </template>

        <template #default="{ collapsed }">
          <UButton
            :label="collapsed ? undefined : 'Search...'"
            icon="i-lucide-search"
            color="neutral"
            variant="outline"
            block
            :square="collapsed"
          >
            <template v-if="!collapsed" #trailing>
              <div class="flex items-center gap-0.5 ms-auto">
                <UKbd value="meta" variant="subtle" />
                <UKbd value="K" variant="subtle" />
              </div>
            </template>
          </UButton>

          <UNavigationMenu :collapsed="collapsed" :items="items[0]" orientation="vertical" />

          <UNavigationMenu :collapsed="collapsed" :items="items[1]" orientation="vertical" class="mt-auto" />
        </template>

        <template #footer="{ collapsed }">
          <UButton
            :avatar="{ src: 'https://github.com/miumerfarooq.png' }"
            :label="collapsed ? undefined : 'Umer'"
            color="neutral"
            variant="ghost"
            class="w-full"
            :block="collapsed"
          />
        </template>
      </UDashboardSidebar>

      <UDashboardPanel>
        <template #header>
          <UDashboardNavbar title="Dashboard" />
        </template>
      </UDashboardPanel>
    </UDashboardGroup>
  </div>
</template>
