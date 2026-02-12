<script setup lang="ts">
import type { DropdownMenuItem } from '@nuxt/ui';

definePageMeta({
  layout: 'dashboard'
})

const open = ref(false)

defineShortcuts({
  n: () => open.value = !open.value
})

const items2 = ref<DropdownMenuItem[][]>([
  [
    {
      label: 'Umer Farooq',
      avatar: {
        src: 'https://github.com/miumerfarooq.png'
      },
      type: 'label'
    }
  ],
  [
    { label: 'Profile', icon: 'i-lucide-user' },
    { label: 'Billing', icon: 'i-lucide-credit-card' },
    { label: 'Settings', icon: 'i-lucide-cog', kbds: [','] },
    { label: 'Keyboard shortcuts', icon: 'i-lucide-monitor' }
  ],
  [
    { label: 'Team', icon: 'i-lucide-users' },
    {
      label: 'Invite users',
      icon: 'i-lucide-user-plus',
      children: [
        [
          { label: 'Email', icon: 'i-lucide-mail' },
          { label: 'Message', icon: 'i-lucide-message-square' }
        ],
        [
          { label: 'More', icon: 'i-lucide-circle-plus' }
        ]
      ]
    },
    {
      label: 'New team',
      icon: 'i-lucide-plus',
      kbds: ['meta', 'n'],
      onSelect() {
        console.log('Invite by link clicked')
      }
    }
  ],
  [
    {
      label: 'GitHub',
      icon: 'i-simple-icons-github',
      to: 'https://github.com/miumerfarooq/school-management-system-frontend-nuxtjs',
      target: '_blank'
    },
    {
      label: 'Support',
      icon: 'i-lucide-life-buoy',
      to: '/docs/components/dropdown-menu'
    },
    {
      label: 'API',
      icon: 'i-lucide-cloud',
      disabled: true
    }
  ],
  [
    {
      label: 'Logout',
      icon: 'i-lucide-log-out',
      kbds: ['shift', 'meta', 'q']
    }
  ]
])
</script>

<template>
  <UDashboardPanel>
    <template #header>
      <UDashboardNavbar title="Dashboard" :ui="{ right: 'gap-3' }">
        <template #leading>
          <UDashboardSidebarCollapse />
        </template>

        <template #right>
          <UTooltip v-model:open="open" text="Notification">
            <UButton color="neutral" variant="ghost" square>
              <UChip color="error" inset>
                <UIcon name="i-lucide-bell" class="size-5 shrink-0" />
              </UChip>
            </UButton>
          </UTooltip>

          <UDropdownMenu :items="items2">
            <UButton icon="i-lucide-plus" size="md" class="rounded-full" />
          </UDropdownMenu>
        </template>
      </UDashboardNavbar>
    </template>
  </UDashboardPanel>
</template>
