---
name: $name
sourceUrl: $sourceUrl
docUrl: $docUrl
---

<script>
  import { mdiAccount } from '@mdi/js';

  import api from '$lib/components/ExpansionPanel.svelte?raw&sveld';
  import ApiDocs from '$lib/components/ApiDocs.svelte';

  import Button from '$lib/components/Button.svelte';
  import ExpansionPanel from '$lib/components/ExpansionPanel.svelte';
  import ListItem from '$lib/components/ListItem.svelte';
  import Preview from '$lib/components/Preview.svelte';
</script>

# Examples

## Simple

<Preview>
  {#each Array(5) as _, i}
    <ExpansionPanel>
      <div slot="trigger" class="flex-1 p-3">Item {i + 1}</div>
      <div>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
        omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
        Inventore laborum rerum at id?
      </div>
    </ExpansionPanel>
  {/each}
</Preview>

## Actions

<Preview>
  {#each Array(5) as _, i}
    <ExpansionPanel>
      <div slot="trigger" class="flex-1 p-3">Item {i + 1}</div>
      <div slot="actions" class="p-2">
        <Button>Action 1</Button>
        <Button>Action 2</Button>
      </div>
      <div>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
        omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
        Inventore laborum rerum at id?
      </div>
    </ExpansionPanel>
  {/each}
</Preview>

## Disabled items

<Preview>
  {#each Array(5) as _, i}
    <ExpansionPanel disabled={i % 2}>
      <div slot="trigger" class="flex-1 p-3">Item {i + 1}</div>
      <div>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
        omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
        Inventore laborum rerum at id?
      </div>
    </ExpansionPanel>
  {/each}
</Preview>

## ListItem trigger

<Preview>
  {#each Array(5) as _, i}
    <ExpansionPanel>
      <ListItem
        slot="trigger"
        title="Item {i + 1}"
        subheading="List Item"
        icon={mdiAccount}
        avatar={{ class: 'bg-gray-400 text-white/90' }}
        class="flex-1"
        noShadow
      />
      <div>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
        omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
        Inventore laborum rerum at id?
      </div>
    </ExpansionPanel>
  {/each}
</Preview>

## Mix ExpansionPanel with ListItem

### first and last items

<Preview>
  <ExpansionPanel>
    <ListItem
      slot="trigger"
      title="Item 1"
      subheading="Expansion Panel"
      icon={mdiAccount}
      avatar={{ class: 'bg-gray-400 text-white/90' }}
      class="flex-1"
      noShadow
    />
    <div>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
      omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
      Inventore laborum rerum at id?
    </div>
  </ExpansionPanel>
  <ListItem
    title="Item 2"
    subheading="List Item"
    icon={mdiAccount}
    avatar={{ class: 'bg-gray-400 text-white/90' }}
  />
  <ExpansionPanel>
    <ListItem
      slot="trigger"
      title="Item 3"
      subheading="Expansion Panel"
      icon={mdiAccount}
      avatar={{ class: 'bg-gray-400 text-white/90' }}
      class="flex-1"
      noShadow
    />
    <div>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
      omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
      Inventore laborum rerum at id?
    </div>
  </ExpansionPanel>
</Preview>

## Mix ExpansionPanel with ListItem

### middle item

<Preview>
  <ListItem
    title="Item 1"
    subheading="List Item"
    icon={mdiAccount}
    avatar={{ class: 'bg-gray-400 text-white/90' }}
  />
  <ExpansionPanel>
    <ListItem
      slot="trigger"
      title="Item 2"
      subheading="Expansion Panel"
      icon={mdiAccount}
      avatar={{ class: 'bg-gray-400 text-white/90' }}
      class="flex-1"
      noShadow
    />
    <div>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Reiciendis quod culpa et, dolores
      omnis, ipsum in perspiciatis porro ut nihil molestiae molestias tenetur delectus velit!
      Inventore laborum rerum at id?
    </div>
  </ExpansionPanel>
  <ListItem
    title="Item 3"
    subheading="List Item"
    icon={mdiAccount}
    avatar={{ class: 'bg-gray-400 text-white/90' }}
  />
</Preview>

# API

<ApiDocs {api} />
