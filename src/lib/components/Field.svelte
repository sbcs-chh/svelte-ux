<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { mdiClose, mdiInformationOutline } from '@mdi/js';
  import { uniqueId } from 'lodash-es';

  import Button from './Button.svelte';
  import Icon from './Icon.svelte';
  import Stack from './Stack.svelte';
  import { cls } from '../utils/styles';

  const dispatch = createEventDispatcher<{
    clear: null;
  }>();

  export let label = '';
  export let value: any = null;
  // export let placeholder = '';
  export let error = '';
  export let hint = '';
  // export let autocomplete = 'off'; // https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete
  // export let multiline = false;
  export let disabled = false;
  export let clearable = false;
  export let base = false;
  export let rounded = false;
  export let filled = false;
  export let dense = false;
  export let icon: string | null = null;
  export let iconRight: string | null = null;
  // export let align: 'left' | 'center' | 'right' = 'left';
  export let shrinkLabel = true; // $$slots.prefix || $$slots.suffix;
  // export let actions: Actions = undefined;
  // export let inputEl: HTMLInputElement | null = null;
  export let center = false;
  export let classes: {
    root?: string;
    container?: string;
  } = {};

  $: hasValue = Array.isArray(value)
    ? value.length > 0
    : !!value /* anything truthy such as object, non-empty string, etc */;
  $: hasLabel = label !== '';

  $: hasPrepend = $$slots.prepend || icon != null;
  $: hasAppend = $$slots.append || iconRight != null || clearable || error;

  $: hStackTemplate = `${hasPrepend ? 'auto' : ''} 1fr ${hasAppend ? ' auto' : ''}`;

  const id = uniqueId('field_');
  let labelEl: HTMLLabelElement | null = null;
</script>

<fieldset
  {disabled}
  class={cls(
    'group',
    error
      ? '[--color:theme(colors.red.500)]'
      : filled
      ? '[--color:theme(colors.gray.600)]'
      : '[--color:theme(colors.accent.500)]',
    disabled && 'opacity-50 pointer-events-none',
    !base && (rounded ? 'rounded-full' : 'rounded'),
    classes.root,
    $$props.class
  )}
>
  <div
    class={cls(
      'border py-0 transition-shadow',
      disabled ? '' : 'hover:shadow',
      disabled ? '' : error ? 'hover:border-red-700' : 'hover:border-gray-700',
      {
        'px-2': !rounded,
        'px-6': rounded && !hasPrepend,
      },
      !base && [rounded ? 'rounded-full' : 'rounded', filled ? 'bg-black/10' : 'bg-white'],
      error ? 'border-red-500' : 'border-black/20',
      'group-focus-within:shadow-md group-focus-within:border-color-var',
      classes.container
    )}
  >
    <Stack horizontal template={hStackTemplate} items="center">
      {#if hasPrepend}
        <div class="prepend whitespace-nowrap flex items-center">
          <slot name="prepend" />

          {#if icon}
            <span class={cls('mr-3', rounded && !$$slots.prepend && 'ml-3')}>
              <Icon path={icon} class="text-black/50" />
            </span>
          {/if}
        </div>
      {/if}

      <Stack stack items="initial" justifyItems="initial" on:click>
        <label
          class={cls(
            'z-[1] flex items-center h-full truncate origin-top-left transition-all duration-200 group-hover:text-gray-700 group-focus-within:text-color-var cursor-pointer group-hover:group-focus-within:text-color-var',
            center && 'justify-center',
            error ? 'text-red-500/80' : 'text-black/50',
            (shrinkLabel || hasValue) && 'shrink'
          )}
          for={id}
          bind:this={labelEl}
        >
          {label}
        </label>

        <div
          class={cls(
            'input flex items-center overflow-hidden',
            hasLabel && 'pt-4',
            dense ? 'my-1' : 'my-2',
            center && 'text-center'
          )}
        >
          <slot name="prefix" />

          <slot {id} />

          <slot name="suffix" />
        </div>
      </Stack>

      {#if hasAppend}
        <div class="append whitespace-nowrap">
          {#if clearable && hasValue}
            <Button
              icon={mdiClose}
              class="text-black/50 p-1"
              on:click={() => {
                value = Array.isArray(value) ? [] : typeof value === 'string' ? '' : null;
                dispatch('clear');
                labelEl.focus();
              }}
            />
          {/if}

          <slot name="append" />

          {#if error}
            <Icon path={mdiInformationOutline} class="text-red-500" />
          {:else if iconRight}
            <Icon path={iconRight} class="text-black/50" />
          {/if}
        </div>
      {/if}
    </Stack>
  </div>
  <div
    class={cls(
      'hint',
      'text-xs ml-2 transition-transform ease-out overflow-hidden origin-top transform group-focus-within:scale-y-100',
      error ? 'text-red-500' : 'text-black/50 scale-y-0'
    )}
  >
    {error || hint}
  </div>

  <slot name="fieldset" />
</fieldset>

<style lang="postcss">
  label {
    /* border: 1px solid rgba(255, 0, 0, 0.5); */
    width: 100%;
  }
  fieldset:focus-within label,
  label.shrink {
    transform: scale(0.75);
    width: 133%; /* offset 75% scale */
    height: 32px;
  }

  .prepend {
    /* background: rgba(0, 255, 0, 0.1); */
  }

  .append {
    /* background: rgba(0, 255, 0, 0.1); */
  }

  :global([slot='prefix']) {
    /* background: rgba(0, 255, 0, 0.1); */
  }

  :global([slot='suffix']) {
    /* background: rgba(0, 255, 0, 0.1); */
  }
</style>
