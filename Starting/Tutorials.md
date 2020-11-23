# Tutorials

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura004.JPG)

So now the Unity comes with lego tutorials. [After setting Unity](Setting%20Unity.md) I'm following them and add any thoughts here.

## Useful info

* There is no autosave. So Ctrl+S. (or file-> save)

* For the camera alt plus left click to rotate view.

* E for rotate object.

* CTRL+P is the shorcut for switch between the play and the edit mode. (kind of useful)

Between the several tutorials you are going to use the _same_ tutorial, so remember to save previous things that you do, because you will need them.

When using the Lego magic bricks you have to put it not only in the lego grid but connected in an specific place.

### Useful view commands

Unity navigation tools ([taken from here](https://learn.unity.com/tutorial/creating-with-lego-tools#5f919faeedbc2a00222cd95b))

*    **Pan:** Select the Hand Tool in the Toolbar (keyboard shortcut **Q**), then click and drag in the Scene view to move your view.

*    **Zoom:** Holding Alt (Windows) or Option (macOS), right-click and drag in the Scene view to zoom.

*    **Orbit:** Holding Alt (Windows) or Option (macOS), left-click and drag to orbit around the current pivot point.

*    **Focus (Frame Select):** When a GameObject is selected, move your cursor into the Scene  view and select the **F** key to focus your view on that GameObject. Important: If your cursor is not in the Scene view (like being on the inspector), Frame Select will not work.


* Flythrough mode

You can also use Flythrough mode to navigate in the Scene view by flying around in first person, which is common in many games. To do this:

    **Click and hold the right mouse button.**
    Use WASD to move the view left/right/forward/backward.
    Use Q and E to move the view up and down.
    Select and hold Shift to move faster.

* Q and W. Switch between "hand and move"



## Other thoughts on the tutorials

In the last tutorial I'm going to try to make a companion bot. There are several and I like them.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura005.JPG)

This was my first try. They reacts to the player but when they tries to move, they doesn't. Tomorrow I will give more love to this fella.

After the basics tutorials of the lego microgame there are more that you can see [here](https://learn.unity.com/project/lego-template?signup=true)

### First problems with the bot

I tried the component of a Golem that it's kind of a robot, but when I connect things to it, it seems that they don't interconnect properly

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura006.JPG)

_the leg is the only part that moves_

So I wil try to do the other tutorials and redo it.


### Swapping the protagonist

This corresponds to this [tutorial](https://learn.unity.com/tutorial/lego-r-mod-change-the-player-minifig)

I had a mistake when setting the new camera. I dragged into the inspector the look at and follow to the same camera. So when I tested the camara is only pointing to the sky.


### Adding more behavior to an enemy (being destroyable)

I added the option to one of the enemys to explode if it's touched.

This is the enemy.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura007.JPG)

_tower of evil_

I had a bug because the bricks weren't connected properly. Also I had to ensure that everything was connected because I tried once and the brick was upside down so the behavior was totally disconnected.

And these are the settings of the touch behavior brick

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura008.JPG)

_so now it looks at you and fires you and gets destroyed if you touch it_


### New bot

So using [this tutorial](https://learn.unity.com/tutorial/lego-r-mod-build-your-own-enemy?uv=2019.4&projectId=5f3cfedbedbc2a002093abe3#5f3d0ca9edbc2a0020e35d17) I added another being in the map.

In this case I just used the starter bricks because when I used a mix of cool ones I couldn't find the object connected in the project = (

And this is the result

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura009.JPG)

_It's called Mari Gertrudis_

I added also to the prefabs and now I have several of these!

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura009b.JPG)

_bop!_

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura010.JPG)

Now there are several of them.

And these instances can be modified so each of them acts differently. Here I add a different behavior brick to each of them.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura011.JPG)

_my buddies_

Now I'm trying to get rid of the behavior bricks using them as script components and not physical (sort of) components. [I'm using this tutorial](https://learn.unity.com/tutorial/lego-mod-behavior-beyond-bricks)

So I made stinky

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura012.JPG)

_Stinky says pop POP_

Remember when adding a script that you might accidentally added to several bricks instead of just one.

When I'm doing the moody sky tutorial, it asks me for downloading and installing some assets. Since they are not explained, I'll do it here for future David.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura013.JPG)

_so installing things, huh?_

## How to add and import an asset from the asset store

In this case (Lego assets available for free in the Unity Store) I go for the addons linked while I'm logged in.

You'll see something like this:

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura014.JPG)

_this is already installed but you get the idea_

And you press add to my stuff/purchase for free blue button.  Then you can open it with unity. It's not yet installed. In unity you'll see a new window of package manager.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura015.JPG)

Now you can download it. (Button on the bottom right) Once you have download it you can import into your project (button next to download)

Then Unity will show you another window to confirm the contents of the package and the route.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura016.JPG)

Just confirm by pressing Import in that window. And now if everything is ok, the content should be in your project like this

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura017.JPG)

_ready to roll!_

Using that tutorial about changing the sky and adding music to the scene I finally put some other colors to the game

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura018.JPG)

_I like it more this way_

And when I finished all the tutorials this is what I left:

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura019.JPG)

Now I'm using the next course. [Starting with unity](https://learn.unity.com/course/getting-started-with-unity?uv=2019.3)

## I don't have the option that the tutorial needs

When I'm doing the course of the platformer (which is the one the more interesting for me). [I see that the Tile Palette to make palettes is not avialable](https://learn.unity.com/tutorial/2d-platformer-challenge-paint-your-level?uv=2019.3&projectId=5c8838feedbc2a0ee1e7e030#5c8932f9edbc2a1410354fda) because... reasons.

So let's try to find out how to make it avialable.

It seems that you need to install [Tilemap](https://docs.unity3d.com/Manual/class-Tilemap.html) to have the option. To install you need to go to the package manager (Window > Package Manager, just bellow Asset Store). Then if you look for Tilemap


![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura020.JPG)

And when you install it you have the option of go to Window > Tile palette.

## Conclusions of the Unity Tutorials (microgames)

I've worked with the microgames of the kart and the 2D microgame.

The Unity microgames tutorials and projects are nice because they give you the feel of doing things and showing them. The bad part is that you just modify things instead of making them. But it's useful, nonetheless.

After doing them I followed the course more "We're putting here a circle" that it's not that fancy but once you've done the microgames it's easier to swallow.

Here is the pachinko animation that I've done.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/pachinko.gif)
