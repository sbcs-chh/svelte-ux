<script lang="ts">
  import { intersection } from '../actions/observer';

  /**
   * Placeholder height.  Should match closely to resulting height to reducing scroll bouncing
   */
  export let height: string | number;

  let show = false;

  type Offset = {
    top?: string;
    bottom?: string;
    left?: string;
    right?: string;
  };

  export let offset: Offset = {};

  // $: if (show) {
  //   console.count('mounting');
  // }
</script>

<div
  use:intersection={{
    rootMargin: `${offset.top ?? '0px'} ${offset.right ?? '0px'} ${offset.bottom ?? '0px'} ${
      offset.left ?? '0px'
    }`,
  }}
  on:intersecting={(e) => {
    if (e.detail.isIntersecting) {
      show = true;
    }
  }}
  style:min-height={typeof height === 'number' ? `${height}px` : height}
  {...$$restProps}
>
  {#if show}
    <slot />
  {/if}
</div>
