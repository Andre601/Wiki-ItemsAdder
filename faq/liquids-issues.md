---
icon: water
---

# Liquids issues

{% hint style="warning" %}
These are all Minecraft bugs I cannot fix. This is how the game works.\
Please do not report these issues.
{% endhint %}

## Liquids do not spread like water!

{% hint style="success" %}
It's working as intended to avoid lag and glitches.\
Use multiple liquid buckets to create a larger liquid area.
{% endhint %}

<figure><img src="../.gitbook/assets/liquids-issues_007.png" alt=""><figcaption></figcaption></figure>

### Custom liquid color mixed with water and vice versa

Custom liquids are not totally colored sometimes, some parts still have vanilla water color.\
This is a limitation of how the game works. I cannot fix this.

<details>

<summary>Technical reason</summary>

Minecraft stores biomes of a chunk in an int\[1024]. 16x16x256=65536, that's way more than 1024. This means that it stores it in some kind of blobs (not sure myself which size they are), so changing specific blocks is sadly not possible. The colours also fade between biomes, so changing small "blobs" always looks weird and the blocks won't have the full colour.

Source: [https://www.spigotmc.org/threads/how-to-create-custom-biomes.512105/page-2#post-4243330](https://www.spigotmc.org/threads/how-to-create-custom-biomes.512105/page-2#post-4243330)

</details>

![](../.gitbook/assets/liquids-issues_004.png)

### I cannot see liquid color at all, even by placing it in a different location

You have to set the biome blend to `5x5` or lower.

#### Bad

<figure><img src="../.gitbook/assets/liquids-issues_005.png" alt=""><figcaption></figcaption></figure>

#### Good

<figure><img src="../.gitbook/assets/liquids-issues_006.png" alt=""><figcaption></figcaption></figure>
