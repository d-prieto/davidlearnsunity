# Setting Unity

Ok, this shouldn't be a bother. But I'm using and old installation of Unity I had and I'll update it as I have the settings today 29/11/2020.


## Setting the Github and these pages

I made this documentation repo because I did [fabacademy](http://fabacademy.org/2020/labs/barcelona/students/david-prieto/) and now I'm used to document things.

If you want more info on how I got into the git thingy, [you can look here](http://fabacademy.org/2020/labs/barcelona/students/david-prieto/assignments/week02/#2-project-management)

Even if I use git as usual, to do this bare website (That I might use or improve in the future) I had installed [GIT](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) (bash and gui) and [tortoise git](https://tortoisegit.org/) (just because it has a direct "clone here") and made a folder to hold everything.

I'm using [Atom](https://atom.io/) as a text editor

I already had an account in github. Then I follow the steps to create a new repository. I'm using markdown files that I write in my computer in Atom and I upload them to this repository.

For creating my local repo I had to copy my ssh key. To do that I think that probably there is a gui bash command. But since I'm to _lazy_ to remember o to look for it in the internet, I opened the git GUI (Graphical User interface) and navigating into those menus in help->show SSH key I found what I needed.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura000.JPG)

_SSH don't share it unless you have to_

Then I set that SSH Key into github so github recognizes this computer and user as _me_. If you do it with other computer you'll need to copy or add another SSH Key.

Now I'm ready to clone the repo. I copied the **HTTPS** option, it doesn't seem to work with SSH.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura001.JPG)

_this is the thing to copy to clone a repo_

Then to clone the repo I made a folder called repo and then go to-> right click in the white space of the folder -> git clone... and then see if everything is ok.

Then I made the folders. And try to make a first try push. It seems that even if git is integrated into atom (that's why I'm using it), you have to login _again_ into Github. At least you only have to do it once.

I also tested how the images are shown and linked so if I push screenshots you can see them nicely.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura002.JPG)

_this is my atomUI and what I see when I document_

## Installing Unity

I said, ok, I have a build (menu->help->about Unity) and check that I have a 2018 build. I guess that there is no auto update. And when I go to the website there are lots of options and... Unity hub?

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura003.JPG)

_lots of options_

For what I see Unity Hub is Unity with _templates_ [here https://forum.unity.com/threads/templates-overview-details-and-request-for-feedback.514369/](https://forum.unity.com/threads/templates-overview-details-and-request-for-feedback.514369/)


There is also a Unity ID. I don't recommend to use a facebook or google account for this but a ad hoc account. I don't want to tell google or facebook _more_ data about me.

So let's create a new account (you have to put a valid email account) and store with chrome, firefox or something else the password.

The new download goes with several micro-projects to play with. Also be aware that you will need lots of space (9 Gb) for this installation. And I guess that these tutorial microprojects are not light also.

![Starting image](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/Starting/images/Captura004.JPG)

_I really didn't expect that_

## Tutorials

I'm following the tutorials (as much as I can) and add any thoughts here.

* There is no autosave. So Ctrl+S. (or file-> save)

* For the camera alt plus left click to rotate view.

* E for rotate object.

* CTRL+P is the shorcut for switch between the play and the edit mode. (kind of useful)

Between the several tutorials you are going to use the _same_ tutorial, so remember to save previous things that you do, because you will need them.

When using the Lego magic bricks you have to put it not only in the lego grid but connected in an specific place.

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



### Useful view commands

Unity navigation tools ([taken from here](https://learn.unity.com/tutorial/creating-with-lego-tools#5f919faeedbc2a00222cd95b))

*    **Pan:** Select the Hand Tool in the Toolbar (keyboard shortcut **Q**), then click and drag in the Scene view to move your view.

*    **Zoom:** Holding Alt (Windows) or Option (macOS), right-click and drag in the Scene view to zoom.

*    **Orbit:** Holding Alt (Windows) or Option (macOS), left-click and drag to orbit around the current pivot point.

*    **Focus (Frame Select):** When a GameObject is selected, move your cursor into the Scene  view and select the **F** key to focus your view on that GameObject. Important: If your cursor is not in the Scene view, Frame Select will not work.


* Flythrough mode

You can also use Flythrough mode to navigate in the Scene view by flying around in first person, which is common in many games. To do this:

    **Click and hold the right mouse button.**
    Use WASD to move the view left/right/forward/backward.
    Use Q and E to move the view up and down.
    Select and hold Shift to move faster.

* Q and W. Switch between "hand and move"


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
