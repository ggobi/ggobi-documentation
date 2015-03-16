# GGobi and GTK 3.0 #

It is time that we start anticipating the arrival of GTK3. No one knows when this will happen, but GTK 2.10 will likely be released early this summer. Here we will attempt to track the progress of GTK, as well as related libraries like GLib and Cairo, and post ideas on how GGobi might best capitalize on upcoming functionality.

## GTK 2.10 ##

### Almost definite features (of interest) ###

  * Notebook tab reordering by dnd
  * Recent file choosing and tracking

(Ok, those are pretty boring)

### Less definite but more significant features ###

  * Cross-platform printing API and widgets based on cairo. Not sure if this is useful given DescribeDisplay plugin.
  * Cairo canvas.

Given the presence of the word 'cairo' in both of those items, it seems clear that if we want to take advantage of them, we should try to modularize our rendering so that we can drop in a cairo renderer at some point. Clearly, GDK will need to give us a glitz surface if we're going to be able to use cairo for anything besides printing or image writing. Of course, we can link into glitz ourselves, but that's inconvenient.

## GTK 3.0 ##

  * OpenGL integration

Another argument for a modular renderer is that eventually we'll want to draw 3D objects, programming directly against the OpenGL API. This functionality is already provided by GtkGLExt and it will be merged into GTK 3.0.