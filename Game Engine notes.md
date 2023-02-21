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

