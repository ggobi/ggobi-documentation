# Building GGobi OS X #

This guide assumes some expertise with the command line.

## Step One: Install dependencies ##

Install the following in the usual mac manner

  * Latest version (>= 2.4) of  [Xcode](http://developer.apple.com/tools/download/), and X11 installed from your install dvd.
  * [MacPorts](http://macports.org/)
  * [R](http://r-project.org) (if installing Rggobi)

Then, from the terminal, run (this will take a while, so you might want to do it overnight):

```
sudo port install gtk2 automake libtool graphviz
ln -s /opt/local/bin/glibtool /opt/local/bin/libtool
ln -s /opt/local/bin/glibtoolize /opt/local/bin/libtoolize
```

(If you are having any problems with these commands, try `sudo port selfupdate` and then repeating)

## Step Two: Build ggobi ##

```
curl http://www.ggobi.org/downloads/ggobi-2.1.5.tar.bz2 -O ggobi.tar.bz2
tar jxf ggobi.tar.bz2
cd ggobi
./configure --enable-debug --with-all-plugins
make
sudo make install
make ggobirc
sudo mkdir -p /etc/xdg/ggobi
sudo cp ggobirc /etc/xdg/ggobi/ggobirc
```

Make sure `/usr/local/bin` is on your path, then you can then run ggobi using `ggobi`