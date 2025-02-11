---
name: $name
sourceUrl: $sourceUrl
docUrl: $docUrl
---

<script>
  import api from '$lib/components/ScrollContainer.svelte?raw&sveld';
  import ApiDocs from '$lib/components/ApiDocs.svelte';

  import Button from '$lib/components/Button.svelte';
  import Preview from '$lib/components/Preview.svelte';
  import ScrollContainer from '$lib/components/ScrollContainer.svelte';
</script>

# Examples

## Basic

<Preview>
  <ScrollContainer class="scroll-mt-6 scroll-mb-6" let:scrollIntoView>
    <Button class="bg-blue-500 hover:bg-blue-600 text-white" on:click={() => scrollIntoView({ block: 'end' })}>Scroll to bottom</Button>
    {#each { length: 100 } as _,i}
      <div>Item: {i + 1}</div>
    {/each}
    <Button class="bg-blue-500 hover:bg-blue-600 text-white" on:click={() => scrollIntoView()}>Scroll to top</Button>
  </ScrollContainer>
</Preview>

# API

<ApiDocs {api} />
