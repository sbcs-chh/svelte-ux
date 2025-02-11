---
component: $component
filename: $filename
description: A list item that provides a standard layout and works best with multiple instances in the same parent element.
---

<script lang="ts">
	import { mdiAccount, mdiChevronRight } from '@mdi/js';

	import api from '$lib/components/ListItem.svelte?raw&sveld';
  import ApiDocs from '$lib/components/ApiDocs.svelte';

	import Button from '$lib/components/Button.svelte';
	import Checkbox from '$lib/components/Checkbox.svelte';
	import Icon from '$lib/components/Icon.svelte';
	import ListItem from '$lib/components/ListItem.svelte';
	import Preview from '$lib/components/Preview.svelte';
	import Radio from '$lib/components/Radio.svelte';
	import { cls } from '$lib/utils/styles';

	let selectedId = 1;
	const choices = [
		{ id: 1, name: 'Allow all actions', description: 'Any action can be used, regardless of who authored it or where it is defined.' },
		{ id: 2, name: 'Disable actions', description: 'The Actions tab is hidden and no workflows can run.' },
		{ id: 3, name: 'Allow local actions only', description: 'Only actions defined in a repository within techniq can be used.' },
		{ id: 4, name: 'Allow select actions', description: 'Only actions that match specified criteria, plus actions defined in a repository within techniq, can be used.' },
	]
</script>

# Examples

## Title only

<Preview>
	<ListItem title="Title" />
</Preview>

## Title with subheading

<Preview>
	<ListItem title="Title" subheading="Subheading" />
</Preview>

## Icon

<Preview>
	<ListItem title="Title" icon={mdiAccount} />
</Preview>

## Icon with subheading

<Preview>
	<ListItem title="Title" subheading="Subheading" icon={mdiAccount} />
</Preview>

## Icon with classes

<Preview>
  <ListItem
    title="Title"
    subheading="Subheading"
    icon={mdiAccount}
    avatar={{ class: 'bg-gray-400 text-white/90' }}
  />
</Preview>

## Actions

<Preview>
  <ListItem title="Title">
    <div slot="actions">
      <Button icon={mdiChevronRight} class="p-2 text-black/50" />
    </div>
  </ListItem>
</Preview>

## Multiple

<Preview>
	<ListItem title="Title" />
	<ListItem title="Title" />
	<ListItem title="Title" />
	<ListItem title="Title" />
</Preview>

## Loading

<Preview>
	<ListItem title="Title" subheading="Subheading" />
	<ListItem title="Title" subheading="Subheading" />
	<ListItem title="Title" subheading="Subheading" loading />
	<ListItem title="Title" subheading="Subheading" />
</Preview>

## Radio Group

### example 1

<Preview>
	<div class="rounded border">
		{#each choices as choice}
			<ListItem
				title={choice.name}
				subheading={choice.description}
				on:click={() => (selectedId = choice.id)}
				class={cls(
					'cursor-pointer',
					'hover:bg-blue-50',
					selectedId == choice.id ? 'bg-blue-50' : ''
				)}
			>
				<div slot="avatar" class="contents">
					<Radio checked={selectedId === choice.id} />
				</div>
			</ListItem>
		{/each}
	</div>
</Preview>

## Radio Group

### example 2

<Preview>
	<div class="grid gap-4">
		{#each choices as choice}
			<div class="elevation-1 rounded">
				<ListItem
					title={choice.name}
					subheading={choice.description}
					on:click={() => (selectedId = choice.id)}
					class={cls(
						'px-8 py-4',
						'cursor-pointer ring ring-inset ring-blue-500 transition-shadow duration-100',
						'hover:bg-blue-50',
						selectedId == choice.id ? 'ring-1 bg-blue-50' : 'ring-0'
					)}
					noShadow
				/>
			</div>
		{/each}
	</div>
</Preview>

### example 3

<Preview>
	<div class="grid gap-4 bg-gray-100 p-4">
		{#each choices as choice}
			<div>
				<ListItem
					title={choice.name}
					subheading={choice.description}
					on:click={() => (selectedId = choice.id)}
					class={cls(
						'px-8 py-4',
						'cursor-pointer transition-shadow duration-100 border',
						'hover:bg-white',
						selectedId == choice.id ? 'bg-white shadow-md' : ''
					)}
					noBackground
					noShadow
				>
					<div slot="actions">
						<Checkbox circle dense checked={selectedId == choice.id} />
					</div>
				</ListItem>
			</div>
		{/each}
	</div>
</Preview>

# API

<ApiDocs {api} />
