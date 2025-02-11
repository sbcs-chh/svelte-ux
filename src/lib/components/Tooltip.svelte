<script context="module" lang="ts">
  let lastShown: Date | null = null;
</script>

<script lang="ts">
  import { fly, fade, scale, slide, blur } from 'svelte/transition';
  import type { Placement } from '@floating-ui/dom';

  import Popover from './Popover.svelte';
  import { cls } from '../utils/styles';

  export let title = '';
  export let open = false;
  export let offset = 0;
  export let delay = 500;
  export let underline = false;
  export let cursor = false;
  export let enabled = true;

  // Popover props
  export let placement: Placement = 'bottom';
  export let autoPlacement = false;
  export let matchWidth: boolean = false;

  $: hasTitle = title || $$slots.title;

  let containerEl: HTMLDivElement;

  let timeoutId;

  function showTooltip(e) {
    if (
      delay === 0 ||
      e instanceof FocusEvent ||
      new Date().valueOf() - lastShown?.valueOf() < 500
    ) {
      // If no delay, focus event, or any tooltips shown in the last 1/2 second, show immediately
      lastShown = new Date();
      open = true;
    } else {
      timeoutId = setTimeout(() => {
        lastShown = new Date();
        open = true;
      }, delay);
    }
  }
  function hideTooltip() {
    clearTimeout(timeoutId);
    if (open) {
      lastShown = new Date();
    }
    open = false;
  }
</script>

{#if enabled}
  <Popover
    anchorEl={containerEl?.firstElementChild}
    {placement}
    {autoPlacement}
    {offset}
    {matchWidth}
    {open}
    class="pointer-events-none"
    {...$$restProps}
  >
    <slot name="title">
      {#if title}
        <div
          class="text-white text-xs bg-gray-900/90 px-2 py-1 rounded whitespace-nowrap"
          transition:fly={{
            x: placement === 'left' ? 6 : placement === 'right' ? -6 : 0,
            y: placement === 'top' ? 6 : placement === 'bottom' ? -6 : 0,
            duration: 300,
          }}
        >
          {title}
        </div>
      {/if}
    </slot>
  </Popover>
{/if}

<div
  class="contents"
  on:mouseenter={showTooltip}
  on:mouseleave={hideTooltip}
  on:focusin={showTooltip}
  on:focusout={hideTooltip}
  bind:this={containerEl}
>
  {#if $$props.class || underline || cursor}
    <span
      class={cls(
        hasTitle && underline && 'border-b border-dotted',
        hasTitle && cursor && 'cursor-help',
        $$props.class
      )}
    >
      <slot />
    </span>
  {:else}
    <slot />
  {/if}
</div>
