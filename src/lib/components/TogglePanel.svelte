<script>
  import { getContext, onDestroy } from 'svelte';

  import { groupKey } from './ToggleGroup.svelte';

  const panel = {};
  const { registerPanel, unregisterPanel, selectedPanel } = getContext(groupKey);

  registerPanel(panel);

  onDestroy(() => {
    unregisterPanel(panel);
  });
</script>

{#if $selectedPanel === panel}
  <slot />
{/if}
