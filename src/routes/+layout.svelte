<script lang="ts">
  import 'prism-themes/themes/prism-vsc-dark-plus.css';

  import AppLayout from '$lib/components/AppLayout.svelte';
  import NavMenu from './_NavMenu.svelte';
</script>

<AppLayout>
  <nav slot="nav" class="nav h-full">
    <NavMenu />
    <!-- Spacer -->
    <div class="h-4" />
  </nav>

  <slot />
</AppLayout>

<style lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  :global(body) {
    @apply bg-black/10;
  }

  :global(h2) {
    @apply text-lg font-semibold mt-8 mb-1 ml-2;
  }
  :global(h2:first-child) {
    @apply mt-0;
  }

  :global(h3) {
    @apply text-xs text-black/50 ml-2 mb-1;
  }
  :global(h2 + h3) {
    @apply -mt-1;
  }
</style>
