---
icon: bow-arrow
---

# My First Bow

{% hint style="danger" %}
**Resourcepack hosting**

Remember to **decide** a [**resourcepack hosting**](../plugin-configuration/resourcepack-hosting/) method **before** you **start**.\
For ItemsAdder 4.0.17+, `simple_self_host` is usually the easiest option. Other providers are explained in the linked hosting guide.
{% endhint %}

{% hint style="warning" %}
It is very important to set the textures/models to your bow item correctly, or you will get missing texture.

<img src="../../.gitbook/assets/bow_006.webp" alt="Custom red bow displaying correctly while being pulled in Minecraft" data-size="original">
{% endhint %}

## Modern configuration for Minecraft 1.21.4+

ItemsAdder 4.0.13+ can assign every bow state explicitly. This avoids relying on filename suffix detection and keeps the normal and pulling models visible in the configuration.

### Bow made from textures

```yaml
info:
  namespace: myitems
items:
  my_bow:
    enabled: true
    name: My Bow
    material: BOW
    graphics:
      textures:
        normal: item/my_bow
        pulling_0: item/my_bow_0
        pulling_1: item/my_bow_1
        pulling_2: item/my_bow_2
```

Place `my_bow.png`, `my_bow_0.png`, `my_bow_1.png` and `my_bow_2.png` in `contents/myitems/textures/item/`.

### Bow made from 3D models

```yaml
info:
  namespace: myitems
items:
  my_3dbow:
    enabled: true
    name: My 3D Bow
    material: BOW
    graphics:
      models:
        normal: item/my_3dbow
        pulling_0: item/my_3dbow_0
        pulling_1: item/my_3dbow_1
        pulling_2: item/my_3dbow_2
```

Place the four model files in `contents/myitems/models/item/`. Their texture references must still include the correct namespace, as explained in the legacy model example below.

## Legacy bow with `.png` images

### Configuration file

{% code title="contents/myitems/example_bows.yml" %}
```yaml
info:
  namespace: myitems
items:
  my_bow:
    enabled: true
    name: My Bow
    resource:
      material: BOW
      generate: true
      texture: item/my_bow.png
```
{% endcode %}

### Texture files

The bow animates as you pull it, this allows you to have a single texture for each of these states.

`contents/myitems/textures/item/`

<div align="left"><figure><img src="../../.gitbook/assets/my-first-bow_001.png" alt="Four bow texture files for the normal and three pulling states"><figcaption>The normal texture and the three pulling-state textures.</figcaption></figure></div>

* `_0` - First pulling state
* `_1` - Second pulling state
* `_2` - Third pulling state

<figure><img src="../../.gitbook/assets/my-first-bow_002.webp" alt="Custom turquoise bow being pulled in Minecraft"><figcaption>The texture-based bow in its pulling state.</figcaption></figure>

## Legacy bow with 3D `.json` models

### Configuration file

{% code title="contents/myitems/example_bows.yml" %}
```yaml
info:
  namespace: myitems
items:
  my_3dbow:
    enabled: true
    name: My 3D Bow
    resource:
      material: BOW
      generate: false
      model_path: item/my_3dbow
```
{% endcode %}

### Models files

`contents/myitems/models/item/`

<div align="left"><figure><img src="../../.gitbook/assets/my-first-bow_003.png" alt="Four JSON model files for the normal and three pulling states"><figcaption>The normal model and its three pulling-state variants.</figcaption></figure></div>

* `_0` - First pulling state
* `_1` - Second pulling state
* `_2` - Third pulling state

Open your models files and update the textures paths. As you can see I updated the namespace.

<figure><img src="../../.gitbook/assets/my-first-bow_002.png" alt="JSON model texture references using the myitems namespace"><figcaption>Texture references inside a bow model file.</figcaption></figure>

Move your textures into the correct namespace, in this case `myitems`.

`contents/myitems/textures/item/`

<figure><img src="../../.gitbook/assets/my-first-bow_004.png" alt="Bow and arrow texture files in the namespace texture folder"><figcaption>Textures used by the custom 3D bow model.</figcaption></figure>

<div><figure><img src="../../.gitbook/assets/my-first-bow_003.webp" alt="Custom 3D bow being pulled in Minecraft"><figcaption>The 3D bow in its pulling state.</figcaption></figure></div>
