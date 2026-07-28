---
icon: bag-shopping
---
# Bundle
Bundles can use different textures or models depending on their current state.

A custom bundle can have four graphical states:

- `normal` - Empty bundle.
- `filled` - Bundle containing at least one item.
- `open_back` - Rear layer rendered when an item inside the bundle is selected.
- `open_front` - Front layer rendered over the selected item.

{% hint style="info" %}
The open bundle is composed by Minecraft using three layers:

1. `open_back`
2. The selected item
3. `open_front`

ItemsAdder preserves the same rendering logic used by vanilla Minecraft.
{% endhint %}

## Creating the textures

Create four transparent PNG textures:

``` text
contents/my_bundle_tutorial/textures/item/bundles/ruby_bundle.png
contents/my_bundle_tutorial/textures/item/bundles/ruby_bundle_filled.png
contents/my_bundle_tutorial/textures/item/bundles/ruby_bundle_open_back.png
contents/my_bundle_tutorial/textures/item/bundles/ruby_bundle_open_front.png
```

The resulting folder structure should look like this:

``` text
contents/
└── my_bundle_tutorial/
    ├── bundles.yml
    └── textures/
        └── item/
            └── bundles/
                ├── ruby_bundle.png
                ├── ruby_bundle_filled.png
                ├── ruby_bundle_open_back.png
                └── ruby_bundle_open_front.png
```

{% hint style="warning" %}
The four textures should use the same resolution and canvas size.

The transparent areas of `open_back` and `open_front` are important because Minecraft renders the selected item between them.
{% endhint %}

### Empty bundle texture

`ruby_bundle.png` is the texture shown when the bundle does not contain any items.

### Filled bundle texture

`ruby_bundle_filled.png` is shown when the bundle contains at least one item.

### Open back texture

`ruby_bundle_open_back.png` contains the rear part of the open bundle.

This layer is rendered behind the selected item.

### Open front texture

`ruby_bundle_open_front.png` contains the front part of the open bundle.

This layer is rendered over the selected item.

## Item configuration

Create the following configuration inside `bundles.yml`:

``` yaml
info:
  namespace: my_bundle_tutorial
items:
  ruby_bundle:
    name: Ruby Bundle
    material: BUNDLE
    graphics:
      textures:
        normal: item/bundles/ruby_bundle
        filled: item/bundles/ruby_bundle_filled
        open_back: item/bundles/ruby_bundle_open_back
        open_front: item/bundles/ruby_bundle_open_front
```

The `.png` extension must not be included in the configuration.

## Texture properties

### `normal`

``` yaml
normal: item/bundles/ruby_bundle
```

This property is required and defines the empty bundle texture.

### `filled`

``` yaml
filled: item/bundles/ruby_bundle_filled
```

This property is optional.

When it is omitted, ItemsAdder uses the `normal` model for both empty and filled bundles.

### `open_back`

``` yaml
open_back: item/bundles/ruby_bundle_open_back
```

This property defines the layer rendered behind the selected item.

For texture-based bundles, ItemsAdder automatically generates a model using:

``` text
minecraft:item/template_bundle_open_back
```

### `open_front`

``` yaml
open_front: item/bundles/ruby_bundle_open_front
```

This property defines the layer rendered in front of the selected item.

For texture-based bundles, ItemsAdder automatically generates a model using:

``` text
minecraft:item/template_bundle_open_front
```

{% hint style="warning" %}
`open_back` and `open_front` are optional, but it is recommended to provide both.

When one of them is missing, the corresponding vanilla bundle layer may be used as fallback.
{% endhint %}

## Testing the bundle

Regenerate the resource pack:

``` text
/iazip
```

Get the custom bundle:

``` text
/iaget my_bundle_tutorial:ruby_bundle
```

Put one or more items inside it.

To see the open textures:

1. Open your inventory.
2. Move the cursor over the filled bundle.
3. Use the mouse wheel to select an item inside the bundle.
4. Minecraft will render the selected item between `open_back` and `open_front`.

{% hint style="info" %}
The open layers are only rendered in the GUI while an item inside the bundle is selected.

When the bundle is rendered in the hand, on the ground or in an item frame, it uses the `normal` or `filled` state.
{% endhint %}

## Using custom models

You can provide JSON models instead of letting ItemsAdder generate them from textures.

``` yaml
info:
  namespace: my_bundle_tutorial

items:
  ruby_bundle:
    name: Ruby Bundle
    material: BUNDLE
    graphics:
      models:
        normal: item/bundles/ruby_bundle
        filled: item/bundles/ruby_bundle_filled
        open_back: item/bundles/ruby_bundle_open_back
        open_front: item/bundles/ruby_bundle_open_front
```

Place the model files inside:

``` text
contents/my_bundle_tutorial/models/item/bundles/
```

The resulting structure should look like this:

``` text
contents/
└── my_bundle_tutorial/
    ├── bundles.yml
    ├── models/
    │   └── item/
    │       └── bundles/
    │           ├── ruby_bundle.json
    │           ├── ruby_bundle_filled.json
    │           ├── ruby_bundle_open_back.json
    │           └── ruby_bundle_open_front.json
    └── textures/
        └── item/
            └── bundles/
                ├── ruby_bundle.png
                ├── ruby_bundle_filled.png
                ├── ruby_bundle_open_back.png
                └── ruby_bundle_open_front.png
```

{% hint style="warning" %}
When using `graphics.models`, ItemsAdder does not generate or modify the supplied model files.

The open models must use the correct vanilla template parents.
{% endhint %}

### Open back model

{% code title="ruby_bundle_open_back.json" %}
```json
{
  "parent": "minecraft:item/template_bundle_open_back",
  "textures": {
    "layer0": "my_bundle_tutorial:item/bundles/ruby_bundle_open_back"
  }
}
```
{% endcode %}

### Open front model

{% code title="ruby_bundle_open_front.json" %}
```json
{
  "parent": "minecraft:item/template_bundle_open_front",
  "textures": {
    "layer0": "my_bundle_tutorial:item/bundles/ruby_bundle_open_front"
  }
}
```
{% endcode %}

## Troubleshooting

### I can only see the normal and filled states

The bundle does not become visually open simply because it contains items.

Open the inventory, hover over the bundle and use the mouse wheel to select one of its contents.

### The open bundle uses vanilla textures

Make sure both properties are configured:

``` yaml
open_back: item/bundles/ruby_bundle_open_back
open_front: item/bundles/ruby_bundle_open_front
```

Then run `/iazip` again and accept the updated resource pack.

### The selected item is not positioned correctly

Make sure the open models use these exact parents:

``` text
minecraft:item/template_bundle_open_back
minecraft:item/template_bundle_open_front
```

Also ensure that the front and back textures use the same canvas size and alignment.

### I see a missing texture

Check that:

- The texture paths match the actual files.
- The `.png` extension is not present in the YAML configuration.
- The namespace is correct.
- All filenames use lowercase characters.
- The resource pack was regenerated after adding the files.

## Done

You now have a custom bundle supporting empty, filled and open states while preserving the vanilla selected-item rendering behavior

