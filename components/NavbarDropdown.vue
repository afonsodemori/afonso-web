<script setup lang="ts">
  import type { DropdownMenuItem } from '@nuxt/ui';
  const { locale, setLocale, t } = useI18n();
  const colorMode = useColorMode();

  const items = computed<DropdownMenuItem[][]>(() => [
    [
      {
        label: t('resume.languages'),
        icon: 'i-lucide-earth',
        children: [
          { code: 'en', label: 'English' },
          { code: 'es', label: 'Español' },
          { code: 'pt', label: 'Português' },
        ].map((lang) => ({
          label: lang.label,
          active: locale.value === lang.code,
          onSelect: () => setLocale(lang.code as 'en' | 'es' | 'pt'),
        })),
      },
      {
        label: t('theme.label'),
        icon: colorMode.preference === 'dark' ? 'i-lucide-moon' : 'i-lucide-sun',
        children: [
          {
            label: t('theme.light'),
            icon: 'i-lucide-sun',
            active: colorMode.preference === 'light',
            onSelect: () => (colorMode.preference = 'light'),
          },
          {
            label: t('theme.dark'),
            icon: 'i-lucide-moon',
            active: colorMode.preference === 'dark',
            onSelect: () => (colorMode.preference = 'dark'),
          },
        ],
      },
    ],
    [
      {
        label: 'LinkedIn',
        icon: 'i-simple-icons-linkedin',
        to: '/linkedin',
        target: '_blank',
      },
      {
        label: 'GitHub',
        icon: 'i-simple-icons-github',
        to: '/github',
        target: '_blank',
      },
    ],
  ]);
</script>

<template>
  <div>
    <UDropdownMenu :items="items">
      <UButton icon="i-lucide-menu" color="neutral" variant="link" size="xl" />
    </UDropdownMenu>
  </div>
</template>

<style scoped>
  div {
    position: absolute;
    top: 0;
    right: 0;
    z-index: 10;
  }

  :deep(button) {
    padding: 0.75rem;
  }
</style>
