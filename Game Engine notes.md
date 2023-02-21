## Windowing
when creating a window for the game to run in, there is this concepet of real
fullscreen vs fake fullscreen. For fake fullscreen the window that is created
will simply just fetch the display widht and height and create a window equal to
those dimensions. But this means that 2 players with different sizes of their
displays will see different things and that is not fair. Instead what is usually
done is that there are some options of resolutions say 800x600 and then we set
the rendering mode to fullscreen. In this way the two players will see the exact
same amount of the map for example but the graphics lib will just stretch the
content to match their respective displays. 


## Double-Buffered rendering
The way most rendering is done is that we have 2 buffers, one is the window into
the game world that the user sees, but there is also the same thing going on
behind that window in what is called the second buffer. We draw all the updates
and new objects into that second buffer and once that is done we swap the
buffers. This is so that the user does not see things being rendered and makes
it so that there is much fewer graphical glitches.


## Game Loop Time Step
We cannot couple the update ticks of state of our game/simulation with how often
a frame is updated. Because that will not be controlled by our engine but rather
by how fast the machine that runs the code is.

Also we cannot either just tell the loop to hold for some time by trying to
figure out a how long each frame should have to render etc, because this will
lead to our engine hogging up cpu resources that are doing nothing instead of
releasing the cpu from the current process so it can do something else and we
will notify the cpu when its time to resume with our process. This way we wont
throw away cycles for nothing.

So what we dont want to think about is: How many pixels per frame. Rather we
want to think in terms of: How many pixels per second. This means that the
objects in the game will move and update in the same way for everyone regardless
if the game runs at 500fps or 60fps, since the game tick, i.e the update
frequency of game state will be tied to real world time (well some approximation
that is good enough for our engine anyway).

So in my game engine I will go with the simplest implementation that is robust
enough for a 2d game engine. Since I will not be doing any heavy physics
simulations yet (maybe in the future when i turn the engine into 3d and decide
that I want it to be able to do good physics simulations) I will go with a
Variable Delta-Time approach.

#### Variable Delta-Time
What we do instead of relying on the number of frames per second that we want is
that we will introduce a time dimension. So what we do in this approach is that
we calculate our Delta-time, which is the difference of time between the last
frame and the current one. We will then use this delta-time as a constant
(although it probably is not a constant value since it will change depending on
what is going on with the cpu and how heavy the stuff that we want to calculate
and render actually is) and multiply all movement of objects in our game with
this constant.

I may want to use the semi-variable approach that is mentioned in the link below
if I see that it is needed.

For diving deeper check this link https://gafferongames.com/post/fix_your_timestep/

---
Status: :🌱:
tags: [[030 Software Development.md]]
date: Tue 21 Feb 2023 17:24:01 CET
