<script context="module">
  // Custom components: https://mdsvex.com/docs#custom-components
  import blockquote from './Blockquote.svelte';
  import a from './Link.svelte';
  import h1 from './Header1.svelte';

  // Used by injected info via svelte preprocessor
  import { mdiCodeTags, mdiFileDocumentEditOutline } from '@mdi/js';
  import Button from '$lib/components/Button.svelte';
  import Tooltip from '$lib/components/Tooltip.svelte';

  export { a, blockquote, h1 };
</script>

<script>
  // frontmatter: https://mdsvex.com/docs#frontmatter-1
  export let name = undefined;
  export let sourceUrl = undefined;
  export let docUrl = undefined;
  export let description = undefined;
</script>

{#if name}
  <div class="flex items-center gap-2">
    <span class="text-2xl font-bold">{name}</span>
    {#if sourceUrl}
      <Tooltip title="View source">
        <Button
          class="text-black/50 p-1"
          icon={mdiCodeTags}
          href="https://github.com/techniq/svelte-ux/blob/master/{sourceUrl}"
          target="_blank"
        />
      </Tooltip>
    {/if}

    {#if docUrl}
      <Tooltip title="Edit this page">
        <Button
          class="text-black/50 p-1"
          icon={mdiFileDocumentEditOutline}
          href="https://github.com/techniq/svelte-ux/blob/master/{docUrl}"
          target="_blank"
        />
      </Tooltip>
    {/if}
  </div>

  {#if description}
    {description}
  {/if}

  <div class="text-xs uppercase text-secondary leading-8 tracking-widest text-black/50 mt-4">
    Contents
  </div>
  <div class="border border-black/20 rounded bg-white">
    <slot name="toc" />
  </div>
{/if}

<slot />
