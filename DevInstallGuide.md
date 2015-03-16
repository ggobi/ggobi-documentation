# Install Ggobi & Rggobi (for developers) #

Requirements:

  * Gtk2
  * [gob2](http://www.jirka.org/gob.html) 2.0.14 (GObject Builder)
  * libxml2
  * [R](http://r-project.org) (if installing Rggobi)
  * [Subversion](http://subversion.tigris.org/)(svn)
  * libtool 1.15.22
  * automake (1.9.6 is good)
  * gettext 0.14.5
  * gtk-doc
  * [Vala](http://live.gnome.org/Vala)
  * libgsf

for Mac specific notes on installing requirements see bottom of page

Steps:

```
svn co http://ggobi.org/svn/ggobi/ggobi/trunk ggobi
cd ggobi
./bootstrap
./configure --enable-debug 
make
```

After the first time run `svn up` then  `make`

You can then run ggobi using `./ggobi`

## Installing rggobi ##

You first must have GGobi installed (eg. `sudo make install`.  Make sure you have the following environmental variables set:

```
DISPLAY=0.0.0.0:0
```

Note: The exact commands depends on what type of shell you are running, so you'd modify the above by either preceding with "setenv " and dropping the "=",  OR "export ".

Then

```
svn co http://www.ggobi.org/svn/ggobi/interface/rggobi/trunk/rggobi 
cd rggobi
aclocal
autoconf # you should only need to run these steps the first time you download it
PKG_CONFIG_PATH=/usr/local/lib/pkgconfig/ R CMD INSTALL .
```

Then run `library(rggobi)` from within R.

## Mac specific notes ##

Make sure you have the latest version (>= 2.4) of  [Xcode](http://developer.apple.com/tools/download/), and X11 installed from your install dvd.

I'd recommend [MacPorts](http://macports.org/) to install the requirements.  After you have installed macports, run the following code:

```
sudo port install gtk2 gtk-doc libxml2 automake libtool graphviz subversion
ln -s /opt/local/bin/glibtool /opt/local/bin/libtool
ln -s /opt/local/bin/glibtoolize /opt/local/bin/libtoolize
```

You will need to install [gob2](http://www.jirka.org/gob.html) by hand (eg. download, `./configure;make;sudo make install`)