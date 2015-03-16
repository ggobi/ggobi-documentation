# Rggobi2 and GLib's upcoming introspection support #

I'm looking for ways to simplify my (coding) life. One possible solution would be to make Rggobi2 a pure R package. This has many benefits, including ease of porting and user extensibility (including access to their GGobi plugins).

About a year ago, a gobject-introspection set of utilities was released. It hasn't made it into GLib/GObject yet, but it might by this summer. Basically, we can load a "blob" of metadata into RGtk2 and have it either generate wrappers on the fly or perform all conversions at invocation time. Either way, we're able to bind to GGobi using only RGtk2.

The hardest part then, besides adding support for introspection in RGtk2, would be to obtain a metadata "blob." Such a thing can be created by using a utility that parses an XML format called GIDL (G Interface Definition Language). There are two such files in existence. One is for the Gdk-Pixbuf library, written for testing. Another guy wrote one for Poppler, a PDF rendering library. I am not sure if he did it by hand or what. My thought was to modify the python scripts from PyGTK that parse standard-style header files (should be produced this way by GOB) so that GIDL is output instead of the "defs" format.

Just some ideas...