---
icon: bow-arrow
---

# My First Bow

{% hint style="danger" %}
**Resourcepack hosting**

Remember to **decide** a [**resourcepack hosting**](../plugin-configuration/resourcepack-hosting/) method **before** you **start**.\
I **advise** you to use **self-host** which is **easier** and **faster**, but you can also use **Dropbox** and similar
{% endhint %}

{% hint style="warning" %}
It is very important to set the textures/models to your bow item correctly, or you will get missing texture.

<img src="../../.gitbook/assets/bow_006.webp" alt="" data-size="original">
{% endhint %}

## Bow with `.png` images

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

<div align="left"><figure><img src="../../.gitbook/assets/my-first-bow_001.png" alt=""><figcaption></figcaption></figure></div>

* `_0` - First pulling state
* `_1` - Second pulling state
* `_2` - Third pulling state

<figure><img src="../../.gitbook/assets/my-first-bow_002.webp" alt=""><figcaption></figcaption></figure>

## Bow with 3D `.json` models

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

<div align="left"><figure><img src="../../.gitbook/assets/my-first-bow_003.png" alt=""><figcaption></figcaption></figure></div>

* `_0` - First pulling state
* `_1` - Second pulling state
* `_2` - Third pulling state

Open your models files and update the textures paths. As you can see I updated the namespace.

<figure><img src="../../.gitbook/assets/my-first-bow_002.png" alt=""><figcaption></figcaption></figure>

Move your textures into the correct namespace, in this case `myitems`.

`contents/myitems/textures/item/`

<figure><img src="../../.gitbook/assets/my-first-bow_004.png" alt=""><figcaption></figcaption></figure>

<div><figure><img src="../../.gitbook/assets/my-first-bow_003.webp" alt=""><figcaption></figcaption></figure></div>
