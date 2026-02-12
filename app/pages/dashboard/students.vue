<script setup lang="ts">
definePageMeta({
  layout: 'dashboard'
})
</script>

<template>
  <UDashboardPanel id="students">
    <template #header>
      <UDashboardNavbar title="Students">
        <template #leading>
          <UDashboardSidebarCollapse />
        </template>
      </UDashboardNavbar>
    </template>
  </UDashboardPanel>
</template>
