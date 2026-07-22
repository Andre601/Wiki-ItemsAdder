---
icon: hand-wave
---

# Hands Equipment

## Show custom entity hands equipment

{% embed url="https://youtu.be/LL0c9U4q6gA" %}

## How to configure hands locations

Open your `.iaentitymodel` model file with **Blockbench**.

Select the base bone of the entity hands.

![](../../.gitbook/assets/hands-equipment_006.png)

Create a new group which will be a child of the hand bone.

![](<../../.gitbook/assets/hands-equipment_010.png>)

Right click on the bone and select "**Bone Config**", in this case `left_hand_slot`

![](<../../.gitbook/assets/hands-equipment_008.png>)

Check the "**Left hand pivot**" option and press "**Confirm**".

![](<../../.gitbook/assets/hands-equipment_009.png>)

The hand pivot bone has a new icon now, as you can see.

![](<../../.gitbook/assets/hands-equipment_011.png>)

![](<../../.gitbook/assets/hands-equipment_007.png>)

![](../../.gitbook/assets/hands-equipment_005.png)

Follow the same steps to specify the right hand, then you have to export the model as usual.

{% content-ref url="advanced-method.md" %}
[advanced-method.md](advanced-method.md)
{% endcontent-ref %}
