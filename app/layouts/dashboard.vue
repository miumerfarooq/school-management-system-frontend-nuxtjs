<script setup lang="ts">
import type { DropdownMenuItem, NavigationMenuItem } from '@nuxt/ui';

defineProps<{
  mode: 'drawer' | 'slideover' | 'modal'
}>()

const open = ref(false)

defineShortcuts({
  n: () => open.value = !open.value
})

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
            :label="collapsed ? undefined : 'Umer Farooq'"
            color="neutral"
            variant="ghost"
            class="w-full"
            :block="collapsed"
          />
        </template>
      </UDashboardSidebar>

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
    </UDashboardGroup>
  </div>
</template>
