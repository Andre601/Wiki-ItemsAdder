# Spear
{% hint style="warning" %}
Requires ItemsAdder 4.0.18-beta-16 or greater.
{% endhint %}

Custom spear graphics are supported for these materials:

- `WOODEN_SPEAR`
- `STONE_SPEAR`
- `COPPER_SPEAR`
- `IRON_SPEAR`
- `GOLDEN_SPEAR`
- `DIAMOND_SPEAR`
- `NETHERITE_SPEAR`

## Spear models

Spears have two model states:

- `normal`: default model used outside the player's hand.
- `in_hand`: model displayed while the spear is held.

The `normal` model is required. If `in_hand` is omitted, ItemsAdder uses `normal` for both states.

## Using custom models

``` yaml
info:
  namespace: my_spears

items:
  ruby_spear:
    name: Ruby Spear
    material: DIAMOND_SPEAR
    graphics:
      models:
        normal: item/ruby_spear
        in_hand: item/ruby_spear_in_hand
```

Place the model files here:

``` text
contents/my_spears/models/item/ruby_spear.json
contents/my_spears/models/item/ruby_spear_in_hand.json
```

Use custom models when you need a 3D model or custom display transformations.

## Using textures only

ItemsAdder can generate both spear models automatically from textures.

``` yaml
info:
  namespace: my_spears

items:
  ruby_spear:
    name: Ruby Spear
    material: DIAMOND_SPEAR
    graphics:
      textures:
        normal: item/ruby_spear
        in_hand: item/ruby_spear_in_hand
```

Place the textures here:

``` text
contents/my_spears/textures/item/ruby_spear.png
contents/my_spears/textures/item/ruby_spear_in_hand.png
```

The generated `in_hand` model automatically uses the correct vanilla spear display transformations.

### Using one texture

You can use the same texture for both states:

``` yaml
graphics:
  texture: item/ruby_spear
```

ItemsAdder generates separate models for `normal` and `in_hand`, both using the specified texture.

## Custom icon

Use `icon` to provide a separate inventory texture:

``` yaml
graphics:
  icon: item/ruby_spear_icon
  textures:
    normal: item/ruby_spear
    in_hand: item/ruby_spear_in_hand
```

Place it here:

``` text
contents/my_spears/textures/item/ruby_spear_icon.png
```

The icon is used in the GUI, on the ground, in item displays and on shelves.

## Testing

Reload ItemsAdder and regenerate the resource pack:

``` text
/iareload
```

Get the item:

``` text
/iaget my_spears:ruby_spear
```

``` yaml
items:
  ruby_spear:
    name: Ruby Spear
    material: DIAMOND_SPEAR
    graphics:
      textures:
        normal: item/ruby_spear
        in_hand: item/ruby_spear_in_hand
```

Place the textures here:

``` text
contents/my_spears/textures/item/ruby_spear.png
contents/my_spears/textures/item/ruby_spear_in_hand.png
```

The generated `in_hand` model automatically uses the correct vanilla spear display transformations.

### Using one texture

You can use the same texture for both states:

``` yaml
graphics:
  texture: item/ruby_spear
```

ItemsAdder generates separate models for `normal` and `in_hand`, both using the specified texture.

## Custom icon

Use `icon` to provide a separate inventory texture:

``` yaml
graphics:
  icon: item/ruby_spear_icon
  textures:
    normal: item/ruby_spear
    in_hand: item/ruby_spear_in_hand
```

Place it here:

``` text
contents/my_spears/textures/item/ruby_spear_icon.png
```

The icon is used in the GUI, on the ground, in item displays and on shelves.

## Testing

Reload ItemsAdder and regenerate the resource pack:

``` text
/iareload
```

Get the item:

``` text
/iaget my_spears:ruby_spear
```

