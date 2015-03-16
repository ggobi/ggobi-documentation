# Quick tasks #

If have an hour or so to spare, you might want to have a go at one of these quick tasks

  * Remove existing code that allows multiple ggobis within an instance (only UI change should be removing new from file menu)
  * Set up makefile.am to build pdfs for distribution (and don't distribute figures)
  * Get rid of ggobi-API.{c,h} by moving functions (and documentation) into the appropriate files
  * Create ggobi.gob and move methods out of ggobi.{c,h}, ggobiClass.{c,h} and ggobiAppClass.c
  * take a GUI related struct out of data.gob and make into a model class and view class (eg. GGobiSubset, GGobiSubsetUI)
  * Refactor something in data.gob.
  * Refactor tour methods to reduce code duplication
  * Document a function
  * Look for functions that have no callers
  * Replace the "splash" screen with a `GtkAboutDialog`
  * Clean up header files (may take more than an hour!)
  * Fix a warning in compilation process

Done for now, but do again in the future

  * Run copy and paste detector (http://pmd.sourceforge.net/cpd.html)