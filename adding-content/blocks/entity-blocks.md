---
icon: block-question
---
# Entity Blocks
# Entity blocks

{% hint style="warning" %}
Requires ItemsAdder 4.0.18+ and Minecraft 1.21.4+ on both the server and client.
{% endhint %}

The `ENTITY` block type renders the custom model using a display while preserving normal full-block collision. It does not consume custom blockstate slots.

> The collision always occupies one complete block, even if the visual model is smaller or has a different shape.

## Creating the content pack

Create the following folders and files:

``` text
contents/my_entity_blocks/
├── configs/
│   └── blocks.yml
└── textures/
    └── block/
        └── ruby_block.png
```

A square `16x16` texture is recommended for a normal cube block.

## Minimal configuration

Create `contents/my_entity_blocks/configs/blocks.yml`:

``` yaml
info:
  namespace: my_entity_blocks

items:
  ruby_block:
    name: Ruby Block

    graphics:
      texture: block/ruby_block

    behaviours:
      block:
        placed_model:
          type: ENTITY
          break_particles: ITEM
```

ItemsAdder automatically generates the cube model from the texture.

## Different textures for each face

Create the six textures inside `textures/block/`, then replace the `graphics` section with:

``` yaml
graphics:
  textures:
    down: block/ruby_block_down
    up: block/ruby_block_up
    north: block/ruby_block_north
    south: block/ruby_block_south
    west: block/ruby_block_west
    east: block/ruby_block_east
```

The `.png` extension is optional.

## Using a custom model

Place the model and its textures in your content pack:

``` text
contents/my_entity_blocks/
├── models/
│   └── block/
│       └── ruby_crate.json
└── textures/
    └── block/
        └── ruby_crate.png
```

Then use the model in the item configuration:

``` yaml
graphics:
  model: block/ruby_crate
```

The model JSON must reference textures using the correct namespace, for example:

``` json
"my_entity_blocks:block/ruby_crate"
```

Generated cube models are recommended when possible because ItemsAdder can optimize groups of compatible adjacent blocks automatically.

## Directional blocks

Add `directional_mode` when the block should rotate based on the face where it is placed:

``` yaml
behaviours:
  block:
    placed_model:
      type: ENTITY
      directional_mode: FURNACE
      break_particles: ITEM
```

Available modes:

| Mode | Rotation |
| --- | --- |
| `FURNACE` | Four horizontal directions |
| `LOG` | Three axes, like a log |
| `DROPPER` | All six directions |
| `ALL` | All six directions with full model rotation |

Directional mode is useful only when the model or its faces are visually different.

A fixed rotation can instead be configured with `rotx` and `roty`:

``` yaml
placed_model:
  type: ENTITY
  rotx: 0
  roty: 90
```

## Fallback block

When the custom display cannot be shown, the player sees a vanilla fallback block. The default is `GRAY_CONCRETE`.

You can choose a different fallback for each block:

``` yaml
behaviours:
  block:
    fallback_vanilla_block: RED_CONCRETE
    placed_model:
      type: ENTITY
      break_particles: ITEM
```

The fallback must be a solid, non-interactable block without gravity. Blocks such as concrete and stone are valid; chests, sand and glass are not.

## Generating and testing

1. Save the configuration and texture files.
2. Run your normal ItemsAdder reload and resource-pack generation command, such as `/iazip`.
3. Make sure the updated resource pack is accepted by the client.
4. Give yourself the block:

``` text
/iaget my_entity_blocks:ruby_block
```

5. Place and break it to verify the model, rotation, particles and collision.

## Server limits

Entity block limits are configured in the main ItemsAdder `config.yml`:

``` yaml
blocks:
  custom:
    entity:
      enabled: true
      render-radius: 48
      max-displays-per-player: 512
      max-blocks-per-chunk: 256
      fallback-vanilla-block: GRAY_CONCRETE
```

`max-blocks-per-chunk` prevents excessive entity blocks from being placed in one chunk. Setting it to `0` disables this placement limit.

Keep the default values unless you have a specific reason to change them.

## Troubleshooting

### The custom model is replaced by a vanilla block

Check that:

- The server and client use Minecraft 1.21.4 or newer.
- Entity blocks are enabled in `config.yml`.
- The block is inside the configured render radius.
- The per-player display limit has not been reached.

Seeing the fallback block outside the render range is expected.

### The texture is missing

Check that:

- The PNG exists inside the namespace's `textures` folder.
- The path in `graphics` is relative to that folder.
- The namespace is correct.
- The updated resource pack was generated and accepted.

For example:

``` yaml
graphics:
  texture: my_entity_blocks:block/ruby_block
```

Corresponding file:

``` text
contents/my_entity_blocks/textures/block/ruby_block.png
```

### The block cannot be placed

The chunk may have reached `max-blocks-per-chunk`. Increase the limit carefully or set it to `0` to disable the limit.

### The model has the wrong orientation

Use a suitable `directional_mode`, or adjust the fixed `rotx` and `roty` values.

