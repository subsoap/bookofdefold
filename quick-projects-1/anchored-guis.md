---
description: >-
  Do you want groups of GUI elements to be anchored to a corner of your game's
  screen? You'll need to do something which may not be obvious to you at first
  to make the GUI elements look right.
---

# Anchored GUIs

When you first attempt to anchor GUI elements to an area to the screen you may do it simply by setting each GUI node to have an X and Y anchor and a pivot. But if you scale the screen you may notice some issues with spacing.

![Unscaled Window](../.gitbook/assets/2018-08-07-14_32_54-anchoredguis.png)

![Scaled Window](../.gitbook/assets/2018-08-07-14_32_46-anchoredguis.png)

As can be seen in the "Scaled Window" image above, the spacing between the nodes is inconsistent with the amount of scaling. 

The fix for this is easy!

For each area of the screen you wish to anchor nodes to, you must create a parent anchor GUI node. 

Create a box node. Set its size mode to manual, and set its size to 0,0,0. This will make it invisible.

![](../.gitbook/assets/2018-08-07-14_36_51-window.png)

Then set the anchor box node to have the anchor type you want. In this case X anchor left, Y anchor top.

![](../.gitbook/assets/2018-08-07-14_41_26-window.png)

Now you can move the box node to the area of the screen you wish to anchor other GUIs to.

![](../.gitbook/assets/2018-08-07-14_39_02-defold-editor-2.0-anchoredguis.png)

Then parent the other elements to this anchor GUI. You'll need to update their positions as they will now be relative to the anchor GUI.

![](../.gitbook/assets/2018-08-07-14_46_34-defold-editor-2.0-anchoredguis.png)

Now when you scale the window the GUI elements will look to be spaced more consistently.

![](../.gitbook/assets/2018-08-07-14_41_59-anchoredguis.png)

You should generally follow this example when anchoring elements to areas of the screen as even in less extreme scaling situations the spacing can look off if you do not. 

Using anchor GUIs can be useful for general GUI organization as well.

