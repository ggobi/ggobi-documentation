# Building GGobi on Windows from Source #

This document attempts to explain how to build GGobi (at least the release branch) for Windows. It assumes that the reader is reasonably familiar with building packages in Linux. This process is reasonably streamlined compared to the past, as the MinGW environment has improved immensely.

## Getting the required tools and libraries: ##

### MinGW: ###
The tools we use to build the GGobi distribution depend
on having [MinGW](http://www.mingw.org)
installed.  MinGW is Minimalist GNU for Windows,
essentially gcc for Windows. An [automatic installer](http://sourceforge.net/projects/mingw/files/Automated%20MinGW%20Installer/mingw-get-inst/) is available. There are options within the installation that allow you to customize which
packages are installed.
Be sure that you install support for the MinGW base tools and C++ (libtool looks for it). You'll also want the Developer Toolkit, which includes things like the GNU autotools.

Start the MinGW Shell.

So that the MinGW aclocal finds the macros we will install, we need to execute the following:
```
echo "/usr/local/share/aclocal" > /mingw/share/aclocal/dirlist
```

You'll also want to delete any files starting with libintl in the /mingw/lib directory. This is so that we link against the intl.dll in /usr/local/bin, the same DLL the GTK+ DLL's are built against. Probably a cleaner way, like not installing gettext with MinGW, but not sure if that is possible through the automatic installer.

### RTools ###

For compiling on 64 bit, we need to download and install the [Rtools](http://cran.cnr.berkeley.edu/bin/windows/Rtools/Rtools215.exe). Yes, GGobi is not based on R, but the main MinGW installation only includes a 32 bit compiler. Rtools provides a compiler that can target both i386 and x64. We could get one elsewhere, but this makes sure that things are consistent with R, which matters e.g. for rggobi. Make sure you let it put itself on the PATH.

### GTK development environment: ###
Download the latest GTK+
[developer bundle](http://www.gtk.org/download/win64.php) and unzip it into `MinGW/msys/1.0/local`. You might need to create the `local` directory. This includes GLib, ATK, Pango, gdk-pixbuf and GTK+ itself.

### Libxml2 ###

For 32 bit, get the libxml2 [binaries](ftp://xmlsoft.org/libxml2/win32/) and their libiconv dependency and unzip them into the same tree as the GTK+ stuff.  Place this [pkg-config file](http://code.google.com/p/ggobi-documentation/downloads/detail?name=libxml-2.0.pc&can=2&q=) into `/usr/local/lib/pkgconfig`. You will need to rename the import library libxml2.lib to libxml2.dll.a, otherwise the linker has issues finding it.

For 64 bit, download the source and build the binary and install it.

### Nullsoft Installer: ###
GGobi uses the nullsoft installation system, so
if you want to build the GGobi installer (exe), download and install the latest [nullsoft installer](http://nsis.sourceforge.net/) now.
You need to place the path to your `makensis.exe` in your `PATH` environment variable.

### gtk-doc ###
If you want to build the abandoned trunk of GGobi, you'll need to fake an [installation](http://www.go-evolution.org/Building_Evolution_on_Windows#Fake_gtk-doc) of gtk-doc.

### Subversion: ###
In order to get the latest source code, you'll need
[subversion](http://subversion.apache.org/packages.html#windows).

## Compilation: ##
Start the MinGW Shell. You will find yourself in your "user" directory.
This is where we will do all of our work. Type
```
svn co svn://ggobi.org/ggobi
```
to grab the entire repository, including Rggobi2, the website, the GGobi book, etc.
If you're not a core GGobi dev or you're only interested in the release branch of GGobi itself,
```
svn co svn://ggobi.org/ggobi/ggobi/branches/ggobi-2.1.4 ggobi
```
should do. Next, switch to the
`~/ggobi/ggobi/trunk` (or `~/ggobi` if you only got GGobi) directory and type:
```
./bootstrap
```
If that worked, the build system is ready to be configured. We first need to make sure that the Rtools binaries are first on the path. It is not possible to pre-configure this, because MinGW will prepend its paths when starting the shell. NOTE: the version of GCC might have changed by the time you read this.
```
export PATH=/c/Rtools/gcc-4.6.3/bin:$PATH
```
Now, we can finally run the configure script. For 32 bit, it is simple as:
```
./configure --with-all-plugins
```
For 64 bit, we need to override the CC environment variable:
```
CC="gcc -m64" ./configure --with-all-plugins
```
and then `make`.

If you have trouble send an [email](mailto:ggobi@googlegroups.com),
complete with the error messages from the shell window. We'll aim to help as
possible.

## Building the Self-installing Executable ##

To create the self-installing GGobi executable, we will use the Nullsoft Scriptable
Installation System.

Run `make win32-installer` to build the setup executable.

# Building RGGobi2 on Windows: #

CRAN currently provides an rggobi binary, so there is really no reason to build rggobi on Windows. The following instructions are obsolete, but might serve as a general guide in a pinch.

Follow the instructions for building ggobi on Windows in the ggobi
distribution files. You'll at least need the same development
environment.

## Obtain necessary files ##
[Download](http://www.ggobi.org/Download) the latest rggobi and
unpack it into your home directory, if you didn't check out the entire GGobi SVN repository.

Building the R documentation requires a latex implementation. Get [MiKTeX](http://www.miktex.org) and put latex.exe on your PATH.

In order to build Windows help for the documentation, you need `hhc.exe`
from the [HTML Help Workshop](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/htmlhelp/html/hwMicrosoftHTMLHelpDownloads.asp) on your path. Yes, I know it's from Microsoft, but you need it.

The R build system requires [ActivePerl](http://www.activestate.com/store/languages/register.plex?id=ActivePerl).
Make sure it (`/c/perl/bin`) is on your path BEFORE the `perl.exe` included with the MSYS DTK by typing:
```
export PATH="/c/Perl/bin:$PATH"
```

You'll also need the [zip](http://gnuwin32.sf.net/packages/zip.htm) utility for compressing the packages.

## Build RGtk2 ##
Rggobi depends on RGtk2.

Get RGtk2 from svn:
```
svn co http://statgraphics.had.co.nz/svn/projects/rgtk2/trunk/RGtk2 RGtk2
```

Now enter the `RGtk2` directory, delete `src/Makevars.win` (it's only for CRAN) and run `./configure`.

Copy `inst/include/RGtk2/gtk.h` to `inst/include/RGtk2/gdk.h`. Remove the `src/RGtk2` file and replace it with a directory of the same name containing the headers in `inst/include/RGtk2`. These steps are necessary, because NTFS does not support symbolic links.

Next, you get to hack out the `cygdrive/` token from the `build` perl script in the R `bin` directory. We're using MSYS, not Cygwin, but R doesn't know that.

Now simply run
```
R CMD build --binary RGtk2
```
and install it through R.

## Build the binary R package ##
First, you need to tell rggobi the location of GGobi:
```
  export GGOBI_ROOT=~/ggobi
```

Now, enter the `rggobi` directory, delete `src/Makevars.win` and run `./configure`.

Remove the `src/rggobi` file and replace it with a directory of the same name containing the headers in `inst/include/rggobi`. Move the `inst/gen/out` .R files to `R`, the .h to `src/rggobi` and the .c `src`, except the files with `Import` in their name need to go to `src/rggobi` and those with `Export` to `src/exports`.

In order to build the vignettes, you need to add `\usepackage{Sweave}` to them and place `Sweave.sty` on your LaTeX search path.

Finally, make sure R is on your path, and in the parent directory, run:
```
  Rcmd build --binary rggobi
```

## Installing the package ##

Install the Rggobi package using the R menu for installing packages.

You should be ready to start it up:

```
> library(rggobi)
> ggobi()
```


---

These notes are by Michael Lawrence.