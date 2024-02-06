# Writing a screensaver for Xscreensaver in Rust

## Working out how to get a simple window

Doing some research I first found this guide to write the screensaver from scratch in C [Tutorial](https://www.diag.uniromal.it/~liberato/screensaver/). This details obtaining the window and drawing to it, the basic C code is as follows:

```C
#include<stdlib.h>
#include<X11/Xlib.h>

#include "vroot.h"
main ()
{
  Display *dpy;

  /* open the display (connect to the X server) */
  dpy = XOpenDisplay (getenv ("DISPLAY"));
  
  /* get the root window */
  root = DefaultRootWindow (dpy);
  
  /* create a GC for drawing in the window */
  g = XCreateGC (dpy, root, 0, NULL);
  
  /* draw something */
  while (1)
    {
      /* draw a square */
      XFillRectangle (dpy, root, g, random()%500, random()%500, 50, 40);


      /* once in a while, clear all */
      if( random()%500<1 )
        XClearWindow(dpy, root);


      /* flush changes and sleep */
      XFlush(dpy);
      usleep (10);
    }
}
```

The main idea behind this is to:

- Connect to the X server
- Get the root window
- Create a graphics context to allow us to draw
- Do any drawing we want

### Implementing this in Rust

X11 module exists for rust, explore this.
