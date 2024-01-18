<script setup lang="ts">
import { useLayout } from '/@src/composable/useLayout'

const { LayoutComponent } = useLayout()

useHead({
  title: 'Luwi - Under The Construction',
  htmlAttrs: {
    lang: 'en-US',
  },
  link: [
    {
      rel: 'icon',
      type: 'image/svg+xml',
      href: '/assets/logo/logo.svg',
    },
    {
      rel: 'alternate icon',
      href: '/assets/logo/logo.svg',
      // href: '/favicon.ico',
      type: 'image/x-icon',
    },
    {
      rel: 'apple-touch-icon',
      // href: '/apple-touch-icon.png',
      href: '/assets/logo/logo.svg',
    },
  ],
  meta: [
    {
      name: 'viewport',
      content: 'width=device-width, initial-scale=1',
    },
  ],
  script: [
    {
      children: `(function () {
  const prefersDark = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches
  const settingRe = /color-schema=([^;]+)/
  const setting = localStorage.getItem('color-schema') || 'system'
  if (setting === 'dark' || (prefersDark && setting !== 'light'))
    document.documentElement.classList.toggle('is-dark', true)
})()`,
    },
  ],
})
</script>

<template>
  <component :is="LayoutComponent" />

  <ClientOnly>
    <!-- <ReloadPrompt app-name="Vulk"> -->
    <template #logo>
      <img src="/assets/logo/logo.svg" alt="logo" width="80" height="80" />
    </template>
    <!-- </ReloadPrompt> -->
  </ClientOnly>
</template>
